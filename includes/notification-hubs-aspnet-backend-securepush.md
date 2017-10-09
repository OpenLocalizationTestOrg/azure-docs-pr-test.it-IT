## <a name="webapi-project"></a>Progetto WebAPI
1. In Visual Studio, aprire hello **AppBackend** progetto creato in hello **notifica utenti** esercitazione.
2. In Notifications.cs, sostituire hello intero **notifiche** classe con hello seguente codice. Impossibile verificare tooreplace hello i segnaposto con la stringa di connessione (con accesso completo) per l'hub di notifica e il nome dell'hub hello. È possibile ottenere questi valori da hello [portale di Azure classico](http://manage.windowsazure.com). Questo modulo rappresenta ora hello sicura notifiche diverse che verranno inviate. In un'implementazione completa, le notifiche di hello verranno archiviate in un database. Per semplicità, in questo caso è archiviarli in memoria.
   
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

1. In NotificationsController.cs, sostituire il codice hello all'interno di hello **NotificationsController** definizione di classe con hello seguente codice. Il componente implementa un modo per la notifica di hello dispositivo tooretrieve hello in modo sicuro e fornisce inoltre un dispositivi tooyour push sicura tootrigger un modo (ai fini di hello di questa esercitazione). Si noti che l'invio di hub di notifica toohello notifica hello, solo è inviare una notifica non elaborata con ID hello di notifica hello (e nessun messaggio effettivo):
   
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


Si noti che hello `Post` metodo ora non invia una notifica di tipo avviso popup. Invia una notifica non elaborata che contiene solo ID di notifica di hello e nessun contenuto riservato. Assicurarsi inoltre che toocomment hello operazione per le piattaforme di hello per cui non sono credenziali configurate su hub di notifica, come si verificheranno errori di invio.

1. Ora si distribuirà nuovamente questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi. Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.
2. Selezionare un sito Web Azure come destinazione di pubblicazione. Accedere con l'account Azure e selezionare un sito Web nuovo o esistente e prendere nota di hello **URL di destinazione** proprietà hello **connessione** scheda. Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione. Fare clic su **Pubblica**.

