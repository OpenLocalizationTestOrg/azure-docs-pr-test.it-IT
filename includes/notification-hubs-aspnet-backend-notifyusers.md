## <a name="create-hello-webapi-project"></a>Creare il progetto WebAPI hello
Verrà creato un nuovo back-end ASP.NET WebAPI in sezioni hello che seguono e disporrà di tre scopi principali:

1. **L'autenticazione dei client**: successive richieste di client tooauthenticate e utente di associare hello con richiesta di hello verrà aggiunto un gestore di messaggi.
2. **Registrazioni di notifica client**: in un secondo momento, si aggiungerà un nuove registrazioni di controller toohandle per le notifiche di tooreceive un client dispositivo. Hello nome utente autenticato verrà aggiunta automaticamente la registrazione di toohello come un [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **L'invio di notifiche tooClients**: in un secondo momento, verrà inoltre aggiunto un tooprovide controller un modo per un tootrigger utente toodevices un push sicura e i client associati a tag hello. 

Hello alla procedura seguente mostra come toocreate hello nuovo back-end WebAPI ASP.NET: 

> [!IMPORTANT]
> Se si utilizza Visual Studio 2015 o versione precedente, prima di iniziare questa esercitazione, assicurarsi di aver installato una versione più recente di hello di hello Gestione pacchetti NuGet. toocheck, avviare Visual Studio. Da hello **strumenti** menu, fare clic su **estensioni e aggiornamenti**. Cercare **Gestione pacchetti NuGet** per la versione di Visual Studio e assicurarsi di disporre hello ultima versione. In caso contrario, disinstallare e reinstallare hello Gestione pacchetti NuGet.
> 
> ![][B4]
> 
> [!NOTE]
> Assicurarsi di aver installato Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/) per la distribuzione del sito Web.
> 
> 

1. Avviare Visual Studio o Visual Studio Express. Fare clic su **Esplora Server** e Accedi tooyour account Azure. Visual Studio sarà necessario toocreate hello sito web di risorse nell'account di accesso.
2. In Visual Studio, fare clic su **File**, quindi fare clic su **New**, quindi **progetto**, espandere **modelli**, **Visual c#**, quindi fare clic su **Web** e **applicazione Web ASP.NET**, nome del tipo hello **AppBackend**, quindi fare clic su **OK**. 
   
    ![][B1]
3. In hello **nuovo progetto ASP.NET** finestra di dialogo, fare clic su **API Web**, quindi fare clic su **OK**.
   
    ![][B2]
4. In hello **configurare App Web di Microsoft Azure** finestra di dialogo, scegliere una sottoscrizione e un **piano di servizio App** è già stato creato. È anche possibile scegliere **creare un nuovo piano di servizio app** e crearne uno dalla finestra di dialogo hello. Per questa esercitazione non è necessario disporre di un database. Dopo aver selezionato il piano di servizio app, fare clic su **OK** progetto hello toocreate.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>L'autenticazione client toohello WebAPI Backend
In questa sezione si creerà una nuova classe di gestore di messaggi denominata **AuthenticationTestHandler** per hello nuovo back-end. Questa classe è derivata da [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) e aggiunta come un gestore di messaggi in modo che può elaborare tutte le richieste pervenute nel back-end hello. 

1. In Esplora soluzioni fare doppio clic su hello **AppBackend** del progetto, fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome nuova classe hello **AuthenticationTestHandler.cs**, fare clic su **Aggiungi** classe hello toogenerate. Questa classe verrà utilizzato tooauthenticate gli utenti che usano *l'autenticazione di base* per semplicità. Tenere presente che l'app può usare qualsiasi schema di autenticazione.
2. In AuthenticationTestHandler.cs, aggiungere hello seguente `using` istruzioni:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. In AuthenticationTestHandler.cs, sostituendo hello `AuthenticationTestHandler` definizione di classe con hello seguente codice. 
   
    Questo gestore autorizzerà richiesta hello quando viene soddisfatte hello e tre le condizioni seguenti:
   
   * richiesta di Hello incluso un *autorizzazione* intestazione. 
   * richiesta di Hello utilizza *base* l'autenticazione. 
   * stringa Hello del nome utente e la stringa di password hello sono hello stessa stringa.
     
     In caso contrario, hello richiesta verrà rifiutata. Non si tratta di un vero approccio di autenticazione e autorizzazione. È un esempio molto semplice per questa esercitazione.
     
     Se il messaggio di richiesta di hello è autenticato e autorizzato per hello `AuthenticationTestHandler`, utente di autenticazione di base hello sarà toohello associata la richiesta corrente su hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Informazioni utente in hello HttpContext verranno utilizzate da un altro controller (RegisterController) tooadd successive un [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello richiesta di registrazione della notifica.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
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
       }
     
     > [!NOTE]
     > **Nota sulla sicurezza**: hello `AuthenticationTestHandler` classe non fornisce l'autenticazione true. È usato toomimic solo l'autenticazione di base e non è protetto. È necessario implementare un meccanismo di autenticazione sicuro nelle applicazioni e nei servizi di produzione.                
     > 
     > 
4. Aggiungere hello seguente codice alla fine hello hello `Register` metodo hello **App_Start/WebApiConfig.cs** gestore di messaggi hello tooregister classe:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Salvare le modifiche.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>La registrazione per le notifiche tramite hello WebAPI Backend
In questa sezione verranno aggiunti che un nuovo toohandle di back-end di WebAPI toohello controller richiede tooregister un utente e dispositivo per le notifiche tramite la libreria client di hello per gli hub di notifica. controller Hello verrà aggiunto un tag di utente per l'utente hello che è stato autenticato e collegato toohello HttpContext da hello `AuthenticationTestHandler`. tag Hello avrà il formato di stringa hello, `"username:<actual username>"`.

1. In Esplora soluzioni fare doppio clic su hello **AppBackend** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.
2. Sul lato sinistro di hello, fare clic su **Online**e cercare **Microsoft.Azure.NotificationHubs** in hello **ricerca** casella.
3. Nell'elenco risultati hello, fare clic su **gli hub di notifica di Microsoft Azure**, quindi fare clic su **installare**. Completare l'installazione di hello, quindi chiudere una finestra di gestione pacchetti NuGet hello.
   
    Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
4. A questo punto si creerà un nuovo file di classe che rappresenta la connessione hello con le notifiche toosend utilizzati hub di notifica. In Esplora soluzioni hello, fare clic sul hello **modelli** cartella, fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome nuova classe hello **Notifications.cs**, quindi fare clic su **Aggiungi** classe hello toogenerate. 
   
    ![][B6]
5. In Notifications.cs, aggiungere hello seguente `using` istruzione all'inizio di hello del file hello:
   
        using Microsoft.Azure.NotificationHubs;
6. Sostituire hello `Notifications` definizione con seguenti hello di classe e rendere segnaposto hello due tooreplace che con stringa di connessione hello (con accesso completo) per l'hub di notifica e hello Nome hub (disponibile all'indirizzo [portale classico di Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Verrà quindi creato un nuovo controller denominato **RegisterController**. In Esplora soluzioni fare doppio clic su hello **controller** cartella, quindi fare clic su **Aggiungi**, quindi fare clic su **Controller**. Fare clic su hello **Web API 2 Controller: vuoto** elemento e quindi fare clic su **Aggiungi**. Nome nuova classe hello **RegisterController**, quindi fare clic su **Aggiungi** toogenerate nuovamente i controller di hello.
   
    ![][B7]
   
    ![][B8]
8. In RegisterController.cs, aggiungere hello seguente `using` istruzioni:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Aggiungere hello seguente codice all'interno di hello `RegisterController` definizione di classe. Si noti che in questo codice, aggiungere un utente per l'utente hello che tratta attaccato toohello HttpContext. utente Hello è stato autenticato e collegato toohello HttpContext dal filtro messaggi hello è stata aggiunta, `AuthenticationTestHandler`. È inoltre possibile aggiungere controlli facoltativo tooverify che hello utente disponga dei diritti tooregister per hello richiesto tag.
   
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
10. Salvare le modifiche.

## <a name="sending-notifications-from-hello-webapi-backend"></a>L'invio di notifiche da hello WebAPI Backend
In questa sezione si aggiunge un nuovo controller che espone un modo per client dispositivi toosend una notifica in base a tag username hello utilizzo libreria Gestione servizio hub di notifica di Azure in hello back-end ASP.NET WebAPI.

1. Creare un altro nuovo controller denominato **NotificationsController**. Creazione di hello esattamente come è stato creato hello **RegisterController** nella sezione precedente hello.
2. In NotificationsController.cs, aggiungere hello seguente `using` istruzioni:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Aggiungere hello seguente metodo toohello **NotificationsController** classe.
   
    Questo codice di inviare un tipo di notifica basato su piattaforma Notification Service (PNS) hello `pns` parametro. Hello valore `to_tag` è usato tooset hello *username* tag messaggio hello. Questo tag deve corrispondere a un tag username di una registrazione dell'hub di notifica attiva. messaggio di notifica Hello è estratto dal corpo hello della richiesta POST per hello e formattato per la destinazione di hello PNS. 
   
    A seconda del servizio notifica piattaforma (PNS) che i dispositivi supportati usano le notifiche di tooreceive hello, notifiche diverse sono supportate con formati diversi. Ad esempio nei dispositivi Windows è possibile usare una [notifica di tipo avviso popup con WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) che non è supportata direttamente da un altro PNS. Il back-end è quindi necessario notifica hello tooformat in una notifica supportata per hello PNS dei dispositivi è pianificare toosupport. Utilizza quindi hello trasmissione API hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
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
4. Premere **F5** toorun hello applicazione e tooensure hello l'accuratezza del lavoro svolto finora. applicazione Hello deve avviare un web browser e visualizzare hello ASP.NET home page. 

## <a name="publish-hello-new-webapi-backend"></a>Pubblicare hello nuovo WebAPI Backend
1. Ora si distribuirà questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi. Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.
2. Selezionare **Servizio app di Microsoft Azure** come destinazione di pubblicazione e quindi fare clic su **Pubblica**. Si aprirà hello Create Service App finestra di dialogo che consente di creare tutti hello necessarie risorse di Azure toorun hello app web ASP.NET in Azure.

    ![][B15]
3. In hello **Crea servizio App** finestra di dialogo, selezionare l'account di Azure. Fare clic su **Modifica tipo** e selezionare **App Web**. Mantenere hello **nome dell'applicazione Web** hello specificato e seleziona **sottoscrizione**, **gruppo di risorse**, e **piano di servizio App**.  Fare clic su **Crea**.

4. Prendere nota di hello **URL del sito** proprietà hello **riepilogo** sezione. Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione. Fare clic su **Pubblica**.

5. Una volta completata la procedura guidata hello, pubblica tooAzure di app web ASP.NET hello e quindi avvia hello app nel browser predefinito hello.  L'applicazione sarà visibile in Servizi app di Azure.

URL di Hello utilizza nome dell'applicazione web hello specificato in precedenza, con http://<app_name>.azurewebsites.net formato hello.

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
