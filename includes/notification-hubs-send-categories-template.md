
In questa sezione viene illustrato come toosend le ultime notizie come tag notifiche modello da un'applicazione console .NET.

Se si usa l'App per dispositivi mobili, vedere toohello [aggiungere notifiche push per App per dispositivi mobili] esercitazione e selezionare la piattaforma nella parte superiore di hello.

Se si desidera toouse Java o PHP vedere troppo[come hub di notifica da Java o PHP toouse]. È possibile inviare notifiche da qualsiasi back-end tramite l'[interfaccia REST degli Hub di notifica].

Ignorare i passaggi 1-3 se è stato creato hello di applicazione console per l'invio di notifiche quando è stata completata [iniziare con gli hub di notifica].

1. In Visual Studio creare una nuova applicazione console in Visual C#:
   
       ![][13]
2. Nel menu principale di Visual Studio hello, fare clic su **strumenti**, **Gestione pacchetti libreria**, e **Package Manager Console**, quindi nella finestra di console hello digitare quanto segue e premere **Immettere**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello [pacchetto NuGet di hub Microsoft.Azure.Notification].
3. Aprire il file di hello Program.cs e aggiungere il seguente hello `using` istruzione:
   
        using Microsoft.Azure.NotificationHubs;
4. In hello `Program` classe, aggiungere al metodo hello o sostituirlo se esiste già:
   
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
   
    Questo codice invia una notifica modello per ognuno dei tag di sei hello nella matrice di stringhe hello. utilizzo di Hello del tag assicura che i dispositivi ricevono notifiche solo per le categorie di hello registrato.
5. In hello di sopra di codice, sostituire hello `<hub name>` e `<connection string with full access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultFullSharedAccessSignature* dal dashboard hello di hub di notifica .
6. Aggiungere hello seguenti righe hello **Main** metodo:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Compilare l'applicazione console hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[iniziare con gli hub di notifica]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interfaccia REST degli Hub di notifica]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[aggiungere notifiche push per App per dispositivi mobili]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[come hub di notifica da Java o PHP toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pacchetto NuGet di hub Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
