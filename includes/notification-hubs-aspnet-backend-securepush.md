## <a name="webapi-project"></a><span data-ttu-id="dfada-101">Progetto WebAPI</span><span class="sxs-lookup"><span data-stu-id="dfada-101">WebAPI Project</span></span>
1. <span data-ttu-id="dfada-102">In Visual Studio, aprire hello **AppBackend** progetto creato in hello **notifica utenti** esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dfada-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="dfada-103">In Notifications.cs, sostituire hello intero **notifiche** classe con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="dfada-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="dfada-104">Impossibile verificare tooreplace hello i segnaposto con la stringa di connessione (con accesso completo) per l'hub di notifica e il nome dell'hub hello.</span><span class="sxs-lookup"><span data-stu-id="dfada-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="dfada-105">È possibile ottenere questi valori da hello [portale di Azure classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="dfada-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="dfada-106">Questo modulo rappresenta ora hello sicura notifiche diverse che verranno inviate.</span><span class="sxs-lookup"><span data-stu-id="dfada-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="dfada-107">In un'implementazione completa, le notifiche di hello verranno archiviate in un database. Per semplicità, in questo caso è archiviarli in memoria.</span><span class="sxs-lookup"><span data-stu-id="dfada-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="dfada-108">In NotificationsController.cs, sostituire il codice hello all'interno di hello **NotificationsController** definizione di classe con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="dfada-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="dfada-109">Il componente implementa un modo per la notifica di hello dispositivo tooretrieve hello in modo sicuro e fornisce inoltre un dispositivi tooyour push sicura tootrigger un modo (ai fini di hello di questa esercitazione).</span><span class="sxs-lookup"><span data-stu-id="dfada-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="dfada-110">Si noti che l'invio di hub di notifica toohello notifica hello, solo è inviare una notifica non elaborata con ID hello di notifica hello (e nessun messaggio effettivo):</span><span class="sxs-lookup"><span data-stu-id="dfada-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="dfada-111">Si noti che hello `Post` metodo ora non invia una notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="dfada-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="dfada-112">Invia una notifica non elaborata che contiene solo ID di notifica di hello e nessun contenuto riservato.</span><span class="sxs-lookup"><span data-stu-id="dfada-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="dfada-113">Assicurarsi inoltre che toocomment hello operazione per le piattaforme di hello per cui non sono credenziali configurate su hub di notifica, come si verificheranno errori di invio.</span><span class="sxs-lookup"><span data-stu-id="dfada-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="dfada-114">Ora si distribuirà nuovamente questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="dfada-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="dfada-115">Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="dfada-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="dfada-116">Selezionare un sito Web Azure come destinazione di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="dfada-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="dfada-117">Accedere con l'account Azure e selezionare un sito Web nuovo o esistente e prendere nota di hello **URL di destinazione** proprietà hello **connessione** scheda. Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dfada-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="dfada-118">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="dfada-118">Click **Publish**.</span></span>

