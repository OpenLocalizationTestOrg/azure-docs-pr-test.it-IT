<span data-ttu-id="e1094-101">In questa sezione viene aggiornato il codice nel progetto di back-end dell'app per dispositivi mobili esistente per inviare una notifica push ogni volta che viene aggiunto un nuovo elemento.</span><span class="sxs-lookup"><span data-stu-id="e1094-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="e1094-102">Questa operazione si basa sulla funzionalità dei [modelli](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) di Hub di notifica di Azure, che abilita i push multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="e1094-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="e1094-103">I diversi client vengono registrati per le notifiche push usando i modelli e un unico push universale può raggiungere tutte le piattaforme client.</span><span class="sxs-lookup"><span data-stu-id="e1094-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="e1094-104">Scegliere una delle seguenti procedure che corrisponde al tipo di progetto di back-end&mdash;, che sia [ back-end .NET](#dotnet) o [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="e1094-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="e1094-105"><a name="dotnet"></a>Progetto di back-end .NET</span><span class="sxs-lookup"><span data-stu-id="e1094-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="e1094-106">In Visual Studio fare clic con il pulsante destro del mouse sul progetto server, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e1094-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="e1094-107">Cercare `Microsoft.Azure.NotificationHubs`, quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="e1094-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="e1094-108">Consente di installare la libreria di Hub di notifica per l'invio di notifiche dal back-end.</span><span class="sxs-lookup"><span data-stu-id="e1094-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="e1094-109">Nel progetto server aprire **Controller** > **TodoItemController.cs** e quindi aggiungere le istruzioni using seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1094-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="e1094-110">Nel metodo **PostTodoItem** aggiungere il codice seguente dopo la chiamata a **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="e1094-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="e1094-111">Ogni volta che viene inserito un nuovo elemento, viene inviata una notifica modello contenente l'elemento item.text.</span><span class="sxs-lookup"><span data-stu-id="e1094-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="e1094-112">Pubblicare di nuovo il progetto server.</span><span class="sxs-lookup"><span data-stu-id="e1094-112">Republish the server project.</span></span>

### <span data-ttu-id="e1094-113"><a name="nodejs"></a>Progetto di back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="e1094-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="e1094-114">Se ancora non è stato fatto, [scaricare il progetto di back-end di avvio rapido](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) oppure usare l'[editor online del Portale di Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="e1094-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="e1094-115">Sostituire il codice esistente nel file todoitem.js con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e1094-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="e1094-116">Ogni volta che viene inserito un nuovo elemento, viene inviata una notifica modello contenente l'elemento item.text.</span><span class="sxs-lookup"><span data-stu-id="e1094-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="e1094-117">Quando si modifica il file nel computer locale, ripubblicare il progetto server.</span><span class="sxs-lookup"><span data-stu-id="e1094-117">When editing the file on your local computer, republish the server project.</span></span>
