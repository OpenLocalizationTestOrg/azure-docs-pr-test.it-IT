
<span data-ttu-id="3a2e2-101">In questa sezione viene illustrato come toosend le ultime notizie come tag notifiche modello da un'applicazione console .NET.</span><span class="sxs-lookup"><span data-stu-id="3a2e2-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="3a2e2-102">Se si usa l'App per dispositivi mobili, vedere toohello [aggiungere notifiche push per App per dispositivi mobili] esercitazione e selezionare la piattaforma nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e2-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="3a2e2-103">Se si desidera toouse Java o PHP vedere troppo[come hub di notifica da Java o PHP toouse].</span><span class="sxs-lookup"><span data-stu-id="3a2e2-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="3a2e2-104">È possibile inviare notifiche da qualsiasi back-end tramite l'[interfaccia REST degli Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="3a2e2-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="3a2e2-105">Ignorare i passaggi 1-3 se è stato creato hello di applicazione console per l'invio di notifiche quando è stata completata [iniziare con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="3a2e2-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="3a2e2-106">In Visual Studio creare una nuova applicazione console in Visual C#:</span><span class="sxs-lookup"><span data-stu-id="3a2e2-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="3a2e2-107">Nel menu principale di Visual Studio hello, fare clic su **strumenti**, **Gestione pacchetti libreria**, e **Package Manager Console**, quindi nella finestra di console hello digitare quanto segue e premere **Immettere**:</span><span class="sxs-lookup"><span data-stu-id="3a2e2-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="3a2e2-108">Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello [pacchetto NuGet di hub Microsoft.Azure.Notification].</span><span class="sxs-lookup"><span data-stu-id="3a2e2-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="3a2e2-109">Aprire il file di hello Program.cs e aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="3a2e2-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="3a2e2-110">In hello `Program` classe, aggiungere al metodo hello o sostituirlo se esiste già:</span><span class="sxs-lookup"><span data-stu-id="3a2e2-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="3a2e2-111">Questo codice invia una notifica modello per ognuno dei tag di sei hello nella matrice di stringhe hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e2-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="3a2e2-112">utilizzo di Hello del tag assicura che i dispositivi ricevono notifiche solo per le categorie di hello registrato.</span><span class="sxs-lookup"><span data-stu-id="3a2e2-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="3a2e2-113">In hello di sopra di codice, sostituire hello `<hub name>` e `<connection string with full access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultFullSharedAccessSignature* dal dashboard hello di hub di notifica .</span><span class="sxs-lookup"><span data-stu-id="3a2e2-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="3a2e2-114">Aggiungere hello seguenti righe hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="3a2e2-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="3a2e2-115">Compilare l'applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e2-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[iniziare con gli hub di notifica]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interfaccia REST degli Hub di notifica]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[aggiungere notifiche push per App per dispositivi mobili]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[come hub di notifica da Java o PHP toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacchetto NuGet di hub Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
