In questa sezione, aggiornare codice nel toosend di progetto back-end di App per dispositivi mobili una notifica push esistenti ogni volta che viene aggiunto un nuovo elemento. Questa è una tecnologia hello [modello](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funzionalità di hub di notifica di Azure, l'abilitazione dei push multipiattaforma. Hello vari client vengono registrati per le notifiche push utilizzando i modelli, e un singolo push universale possono ottenere tooall piattaforme client.

Scegliere una delle hello, seguire le procedure seguenti che corrisponde al tipo di progetto back-end&mdash;entrambi [.NET di back-end](#dotnet) o [Node.js back-end](#nodejs).

### <a name="dotnet"></a>Progetto di back-end .NET
1. In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**. Cercare `Microsoft.Azure.NotificationHubs`, quindi fare clic su **Installa**. Libreria di hello hub di notifica per l'invio di notifiche dal back-end vengono installati.
2. Nel progetto server hello aprire **controller** > **TodoItemController.cs**e aggiungere hello seguenti istruzioni using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. In hello **PostTodoItem** metodo, aggiungere hello seguente codice dopo la chiamata hello troppo**InsertAsync**:  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Consente di inviare una notifica di modello che contiene l'elemento hello. Testo quando viene inserito un nuovo elemento.
4. Ripubblicare progetto server hello.

### <a name="nodejs"></a>Progetto di back-end Node.js
1. Se non è già fatto, [Scarica progetto back-end di avvio rapido hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), o altrimenti utilizzare hello [editor online nel portale di Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Sostituire il codice esistente in todoitem.js hello con seguenti hello:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    Consente di inviare una notifica di modello che contiene item.text hello quando viene inserito un nuovo elemento.
3. Quando si modifica il file hello nel computer locale, pubblicare di nuovo progetto server hello.
