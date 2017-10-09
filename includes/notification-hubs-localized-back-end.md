



<span data-ttu-id="fa2f0-101">Quando si inviano notifiche di modello che è necessario solo un set di proprietà tooprovide, in questo caso Microsoft invierà set hello di proprietà contenenti versione localizzata di hello delle news corrente hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa2f0-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="fa2f0-102">Questa sezione viene illustrato come le notifiche di toosend tramite un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="fa2f0-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="fa2f0-103">Hello incluso codice trasmissioni tooboth Windows Store e i dispositivi iOS, poiché back-end hello possibile trasmettere tooany dei dispositivi hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="fa2f0-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="fa2f0-104">notifiche di toosend tramite un'applicazione console c#</span><span class="sxs-lookup"><span data-stu-id="fa2f0-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="fa2f0-105">Modificare hello `SendTemplateNotificationAsync` metodo nell'applicazione console hello creato in precedenza con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="fa2f0-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="fa2f0-106">Si noti come in questo caso esiste alcuna necessità toosend più notifiche per piattaforme e impostazioni locali diverse.</span><span class="sxs-lookup"><span data-stu-id="fa2f0-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

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


<span data-ttu-id="fa2f0-107">Si noti che questa chiamata semplice recapiterà troppo dato localizzata hello notizie**tutti** dei dispositivi, indipendentemente dalla piattaforma hello, come l'Hub di notifica si basa e recapita hello corretto i dispositivi di payload native tooall hello sottoscritto tooa tag specifico.</span><span class="sxs-lookup"><span data-stu-id="fa2f0-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="fa2f0-108">Invia notifica hello con i servizi mobili</span><span class="sxs-lookup"><span data-stu-id="fa2f0-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="fa2f0-109">Nell'utilità di pianificazione del servizio Mobile, è possibile utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="fa2f0-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

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


