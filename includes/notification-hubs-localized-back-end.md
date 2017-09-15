



<span data-ttu-id="f2cb6-101">Quando si inviano notifiche modello, è necessario solo fornire un set di proprietà. In questo caso verrà inviato il set di proprietà contenente la versione localizzata delle notizie correnti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f2cb6-101">When you send template notifications you only need to provide a set of properties, in our case we will send the set of properties containing the localized version of the current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="f2cb6-102">In questa sezione viene illustrato come inviare notifiche tramite un’app console</span><span class="sxs-lookup"><span data-stu-id="f2cb6-102">This section shows how to send notifications using a console app</span></span>

<span data-ttu-id="f2cb6-103">Il codice incluso trasmette le notifiche sia Windows Store che a dispositivi iOS, poiché il back-end è in grado di trasmettere a qualsiasi dispositivo supportato.</span><span class="sxs-lookup"><span data-stu-id="f2cb6-103">The included code broadcasts to both Windows Store and iOS devices, since the backend can broadcast to any of the supported devices.</span></span>

### <a name="to-send-notifications-using-a-c-console-app"></a><span data-ttu-id="f2cb6-104">Per inviare notifiche tramite un'app console C#</span><span class="sxs-lookup"><span data-stu-id="f2cb6-104">To send notifications using a C# console app</span></span>
<span data-ttu-id="f2cb6-105">Modificare il metodo `SendTemplateNotificationAsync` nell'app console creata in precedenza con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="f2cb6-105">Modify the `SendTemplateNotificationAsync` method in the console app you previously created with the following code.</span></span> <span data-ttu-id="f2cb6-106">Si noti come in questo caso non sia necessario inviare più notifiche per impostazioni locali e piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="f2cb6-106">Notice how in this case there is no need to send multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending the notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and the proper tags will receive the notifications. 
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


<span data-ttu-id="f2cb6-107">Si noti che questa semplice chiamata distribuirà la notizia localizzata a **tutti** i dispositivi, indipendentemente dalla piattaforma, in quanto l'Hub di notifica crea il payload nativo corretto e lo distribuisce a tutti i dispositivi che hanno sottoscritto un tag specifico.</span><span class="sxs-lookup"><span data-stu-id="f2cb6-107">Note that this simple call will deliver the localized piece of news to **all** your devices, irrespective of the platform, as your Notification Hub builds and delivers the correct native payload to all the devices subscribed to a specific tag.</span></span>

### <a name="sending-the-notification-with-mobile-services"></a><span data-ttu-id="f2cb6-108">Invio della notifica con Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="f2cb6-108">Sending the notification with Mobile Services</span></span>
<span data-ttu-id="f2cb6-109">Nell'utilità di pianificazione di Servizi mobili, è possibile utilizzare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="f2cb6-109">In your Mobile Service scheduler, you can use the following script:</span></span>

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


