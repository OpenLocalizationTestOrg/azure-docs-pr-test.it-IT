



Quando si inviano notifiche di modello che è necessario solo un set di proprietà tooprovide, in questo caso Microsoft invierà set hello di proprietà contenenti versione localizzata di hello delle news corrente hello, ad esempio:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Questa sezione viene illustrato come le notifiche di toosend tramite un'applicazione console

Hello incluso codice trasmissioni tooboth Windows Store e i dispositivi iOS, poiché back-end hello possibile trasmettere tooany dei dispositivi hello è supportato.

### <a name="toosend-notifications-using-a-c-console-app"></a>notifiche di toosend tramite un'applicazione console c#
Modificare hello `SendTemplateNotificationAsync` metodo nell'applicazione console hello creato in precedenza con hello seguente codice. Si noti come in questo caso esiste alcuna necessità toosend più notifiche per piattaforme e impostazioni locali diverse.

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


Si noti che questa chiamata semplice recapiterà troppo dato localizzata hello notizie**tutti** dei dispositivi, indipendentemente dalla piattaforma hello, come l'Hub di notifica si basa e recapita hello corretto i dispositivi di payload native tooall hello sottoscritto tooa tag specifico.

### <a name="sending-hello-notification-with-mobile-services"></a>Invia notifica hello con i servizi mobili
Nell'utilità di pianificazione del servizio Mobile, è possibile utilizzare hello lo script seguente:

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


