<span data-ttu-id="a9f70-101">In questa sezione, aggiornare codice nel toosend di progetto back-end di App per dispositivi mobili una notifica push esistenti ogni volta che viene aggiunto un nuovo elemento.</span><span class="sxs-lookup"><span data-stu-id="a9f70-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="a9f70-102">Questa è una tecnologia hello [modello](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funzionalità di hub di notifica di Azure, l'abilitazione dei push multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="a9f70-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="a9f70-103">Hello vari client vengono registrati per le notifiche push utilizzando i modelli, e un singolo push universale possono ottenere tooall piattaforme client.</span><span class="sxs-lookup"><span data-stu-id="a9f70-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="a9f70-104">Scegliere una delle hello, seguire le procedure seguenti che corrisponde al tipo di progetto back-end&mdash;entrambi [.NET di back-end](#dotnet) o [Node.js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="a9f70-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="a9f70-105"><a name="dotnet"></a>Progetto di back-end .NET</span><span class="sxs-lookup"><span data-stu-id="a9f70-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="a9f70-106">In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="a9f70-107">Cercare `Microsoft.Azure.NotificationHubs`, quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="a9f70-108">Libreria di hello hub di notifica per l'invio di notifiche dal back-end vengono installati.</span><span class="sxs-lookup"><span data-stu-id="a9f70-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="a9f70-109">Nel progetto server hello aprire **controller** > **TodoItemController.cs**e aggiungere hello seguenti istruzioni using:</span><span class="sxs-lookup"><span data-stu-id="a9f70-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="a9f70-110">In hello **PostTodoItem** metodo, aggiungere hello seguente codice dopo la chiamata hello troppo**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="a9f70-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="a9f70-111">Consente di inviare una notifica di modello che contiene l'elemento hello. Testo quando viene inserito un nuovo elemento.</span><span class="sxs-lookup"><span data-stu-id="a9f70-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="a9f70-112">Ripubblicare progetto server hello.</span><span class="sxs-lookup"><span data-stu-id="a9f70-112">Republish hello server project.</span></span>

### <span data-ttu-id="a9f70-113"><a name="nodejs"></a>Progetto di back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="a9f70-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="a9f70-114">Se non è già fatto, [Scarica progetto back-end di avvio rapido hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), o altrimenti utilizzare hello [editor online nel portale di Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="a9f70-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="a9f70-115">Sostituire il codice esistente in todoitem.js hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a9f70-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="a9f70-116">Consente di inviare una notifica di modello che contiene item.text hello quando viene inserito un nuovo elemento.</span><span class="sxs-lookup"><span data-stu-id="a9f70-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="a9f70-117">Quando si modifica il file hello nel computer locale, pubblicare di nuovo progetto server hello.</span><span class="sxs-lookup"><span data-stu-id="a9f70-117">When editing hello file on your local computer, republish hello server project.</span></span>
