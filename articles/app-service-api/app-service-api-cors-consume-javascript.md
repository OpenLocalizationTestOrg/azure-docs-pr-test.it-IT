---
title: supporto aaaCORS nel servizio App | Documenti Microsoft
description: Informazioni di supporto delle toouse CORS in Azure App Service di Azure.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="249ca-103">Utilizzare un'app per le API da JavaScript tramite CORS</span><span class="sxs-lookup"><span data-stu-id="249ca-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="249ca-104">Servizio App offre supporto incorporato per [tra condivisione risorse origini (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), che consente di JavaScript client toomake domini chiama tooAPIs che sono ospitati in App per le API.</span><span class="sxs-lookup"><span data-stu-id="249ca-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="249ca-105">Servizio App consente di configurare CORS accesso tooyour API senza scrivere codice nell'API.</span><span class="sxs-lookup"><span data-stu-id="249ca-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="249ca-106">Questo articolo contiene due sezioni:</span><span class="sxs-lookup"><span data-stu-id="249ca-106">This article contains two sections:</span></span>

* <span data-ttu-id="249ca-107">Hello [come tooconfigure CORS](#corsconfig) sezione viene illustrato in generale come tooconfigure CORS per qualsiasi app per le API, l'app web o app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="249ca-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="249ca-108">Si applica ugualmente tooall Framework supportati dal servizio App, inclusi .NET, Node.js e Java.</span><span class="sxs-lookup"><span data-stu-id="249ca-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="249ca-109">A partire da hello [continuare esercitazioni su Guida introduttiva di .NET hello](#tutorialstart) sezione, articolo hello è un'esercitazione che illustra il supporto CORS dalla compilazione in quanto configurato nel [hello prima App per le API esercitazione introduttiva ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="249ca-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="249ca-110"><a id="corsconfig"></a>Come tooconfigure CORS nel servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="249ca-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="249ca-111">È possibile configurare CORS nel portale di Azure hello o utilizzando [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) strumenti.</span><span class="sxs-lookup"><span data-stu-id="249ca-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="249ca-112">Configurare CORS in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="249ca-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="249ca-113">In un browser andare toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="249ca-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="249ca-114">Fare clic su **servizi App**, quindi fare clic su nome hello dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="249ca-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Selezionare un'app per le API nel portale](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="249ca-116">In hello **impostazioni** pannello visualizzato a destra toohello di hello **app per le API** blade, hello trova **API** sezione e quindi fare clic su **CORS**.</span><span class="sxs-lookup"><span data-stu-id="249ca-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Selezionare CORS nel pannello Impostazioni](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="249ca-118">Nella casella di testo hello immettere hello URL o URL che si desidera tooallow JavaScript chiamate toocome da.</span><span class="sxs-lookup"><span data-stu-id="249ca-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="249ca-119">Ad esempio, se è stata distribuita l'app web di JavaScript applicazione tooa denominato todolistangular, immettere "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="249ca-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="249ca-120">In alternativa, è possibile immettere toospecify un asterisco (*) che vengono accettati tutti i domini di origine.</span><span class="sxs-lookup"><span data-stu-id="249ca-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="249ca-121">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="249ca-121">Click **Save**.</span></span>
   
   ![Fare clic su Salva.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="249ca-123">Dopo aver fatto clic **salvare**, hello API app accetterà JavaScript chiamate da hello specificato l'URL.</span><span class="sxs-lookup"><span data-stu-id="249ca-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="249ca-124">Configurare CORS con gli strumenti di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="249ca-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="249ca-125">È anche possibile configurare CORS per un'app per le API tramite [modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) in strumenti da riga di comando, ad esempio [Azure PowerShell](/powershell/azureps-cmdlets-docs) hello e [CLI di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="249ca-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="249ca-126">Per un esempio di un modello di gestione risorse di Azure che consente di impostare proprietà CORS hello, aprire hello [file azuredeploy.json nel repository di hello per l'applicazione di esempio dell'esercitazione](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="249ca-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="249ca-127">Individuare la sezione hello del modello di hello simile al seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="249ca-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="249ca-128"><a id="tutorialstart"></a>Continuare l'esercitazione Introduzione a .NET di hello</span><span class="sxs-lookup"><span data-stu-id="249ca-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="249ca-129">Se si segue hello Node.js o Java introduttivi serie per App per le API, è necessario completata hello recupero serie avviata.</span><span class="sxs-lookup"><span data-stu-id="249ca-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="249ca-130">Ignorare toohello [passaggi successivi](#next-steps) sezione toofind suggerimenti per l'apprendimento ulteriormente App per le API.</span><span class="sxs-lookup"><span data-stu-id="249ca-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="249ca-131">è una continuazione di hello serie introduttivi .NET Hello parte restante di questo articolo e si presuppone che sia completata correttamente [prima esercitazione hello](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="249ca-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="249ca-132">Distribuire hello ToDoListAngular progetto tooa nuova app web</span><span class="sxs-lookup"><span data-stu-id="249ca-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="249ca-133">In [prima esercitazione hello](app-service-api-dotnet-get-started.md), un'applicazione di livello intermedio API e un'app di API di livello dati sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="249ca-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="249ca-134">In questa esercitazione creerai un'app web di applicazione a pagina singola (SPA) hello chiamate API di livello intermedio app.</span><span class="sxs-lookup"><span data-stu-id="249ca-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="249ca-135">È possibile hello SPA toowork tooenable CORS nel livello intermedio hello app per le API.</span><span class="sxs-lookup"><span data-stu-id="249ca-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="249ca-136">In hello [l'applicazione di esempio ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), progetto ToDoListAngular hello è un semplice client AngularJS che chiama progetto API Web ToDoListAPI di livello intermedio hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="249ca-137">il codice JavaScript in hello Hello *app/scripts/todoListSvc.js* file chiama API hello utilizzando provider HTTP AngularJS hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="249ca-138">Creare una nuova app web per il progetto ToDoListAngular hello</span><span class="sxs-lookup"><span data-stu-id="249ca-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="249ca-139">Hello procedure toocreate una nuova app web di servizio App e distribuire un progetto tooit è toowhat simile per cui si è visto [la creazione e distribuzione di un'applicazione API nella prima esercitazione di hello in questa serie](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="249ca-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="249ca-140">è di sola differenza è il tipo di app hello Hello **App Web** anziché **App per le API**.</span><span class="sxs-lookup"><span data-stu-id="249ca-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="249ca-141">Per le catture di schermata delle finestre di dialogo hello, vedere</span><span class="sxs-lookup"><span data-stu-id="249ca-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="249ca-142">In **Esplora**, fare clic sul progetto ToDoListAngular hello e quindi fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="249ca-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="249ca-143">In hello **profilo** scheda di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="249ca-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="249ca-144">In hello **servizio App** la finestra di dialogo, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="249ca-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="249ca-145">In hello **Hosting** scheda di hello **Crea servizio App** finestra di dialogo immettere un **nome dell'applicazione Web** che sia univoco in hello *azurewebsites.net* dominio.</span><span class="sxs-lookup"><span data-stu-id="249ca-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="249ca-146">Scegliere hello Azure **sottoscrizione** desiderato toowork con.</span><span class="sxs-lookup"><span data-stu-id="249ca-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="249ca-147">In hello **gruppo di risorse** elenco a discesa scegliere hello stesso gruppo di risorse creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="249ca-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="249ca-148">In hello **piano di servizio App** elenco a discesa scegliere hello stesso piano creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="249ca-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="249ca-149">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="249ca-149">Click **Create**.</span></span>
   
    <span data-ttu-id="249ca-150">Visual Studio crea app web hello, crea un profilo di pubblicazione per tale e Visualizza hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="249ca-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="249ca-151">Non è ancora il momento di fare clic su **Pubblica** .</span><span class="sxs-lookup"><span data-stu-id="249ca-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="249ca-152">Nella seguente sezione di hello, configurare hello nuova app toocall hello API di livello intermedio app web è in esecuzione nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="249ca-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="249ca-153">Impostare l'URL di livello intermedio hello nelle impostazioni app web</span><span class="sxs-lookup"><span data-stu-id="249ca-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="249ca-154">Passare toohello [portale di Azure](https://portal.azure.com/), quindi passare toohello **App Web** pannello per l'app web hello creata dal progetto di toohost hello TodoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="249ca-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="249ca-155">Fare clic su **Impostazioni > Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="249ca-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="249ca-156">In hello **impostazioni App** sezione, aggiungere il seguente hello chiave e il valore:</span><span class="sxs-lookup"><span data-stu-id="249ca-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="249ca-157">Chiave</span><span class="sxs-lookup"><span data-stu-id="249ca-157">Key</span></span> | <span data-ttu-id="249ca-158">Valore</span><span class="sxs-lookup"><span data-stu-id="249ca-158">Value</span></span> | <span data-ttu-id="249ca-159">Esempio</span><span class="sxs-lookup"><span data-stu-id="249ca-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="249ca-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="249ca-160">toDoListAPIURL</span></span> |<span data-ttu-id="249ca-161">https://{nome dell'app per le API di livello intermedio}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="249ca-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="249ca-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="249ca-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="249ca-163">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="249ca-163">Click **Save**.</span></span>
   
    <span data-ttu-id="249ca-164">Quando l'esecuzione del codice hello in Azure, questo valore esegue l'override URL localhost hello in hello *Web. config* file.</span><span class="sxs-lookup"><span data-stu-id="249ca-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="249ca-165">codice Hello che ottiene il valore di impostazione hello è *cshtml*:</span><span class="sxs-lookup"><span data-stu-id="249ca-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="249ca-166">codice Hello *todoListSvc.js* Usa impostazione hello:</span><span class="sxs-lookup"><span data-stu-id="249ca-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="249ca-167">Distribuire hello ToDoListAngular web progetto toohello nuova app web</span><span class="sxs-lookup"><span data-stu-id="249ca-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="249ca-168">In Visual Studio, in hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="249ca-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="249ca-169">Visual Studio distribuisce hello ToDoListAngular progetto toohello nuova app web e apre un browser toohello URL hello web app.</span><span class="sxs-lookup"><span data-stu-id="249ca-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="249ca-170">Testare l'applicazione hello senza CORS abilitato</span><span class="sxs-lookup"><span data-stu-id="249ca-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="249ca-171">Nel browser gli strumenti di sviluppo, aprire la finestra di Console hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="249ca-172">Nella finestra del browser hello che visualizza hello UI AngularJS, fare clic su hello **tooDo elenco** collegamento.</span><span class="sxs-lookup"><span data-stu-id="249ca-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="249ca-173">Hello codice JavaScript tenta di livello intermedio toocall hello app per le API, ma hello riesce per mancanza di front-end hello è in esecuzione in un dominio diverso hello nuovamente finale.</span><span class="sxs-lookup"><span data-stu-id="249ca-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="249ca-174">finestra di Console degli strumenti per sviluppatori del browser Hello viene visualizzato un messaggio di errore cross-origin.</span><span class="sxs-lookup"><span data-stu-id="249ca-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Messaggio di errore tra le origini](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="249ca-176">Configurare CORS per il livello intermedio di hello app per le API</span><span class="sxs-lookup"><span data-stu-id="249ca-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="249ca-177">In questa sezione, configurare impostazione di CORS hello in Azure per il livello intermedio di hello app ToDoListAPI API.</span><span class="sxs-lookup"><span data-stu-id="249ca-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="249ca-178">Questa impostazione consentirà hello intermedio app tooreceive JavaScript chiamate all'API da un'app web hello creato per il progetto ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="249ca-179">In un browser, visitare toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="249ca-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="249ca-180">Fare clic su **servizi App**, quindi fare clic su app hello API ToDoListAPI (intermedio).</span><span class="sxs-lookup"><span data-stu-id="249ca-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Selezionare un'app per le API nel portale](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="249ca-182">In hello **impostazioni** pannello visualizzato a destra toohello di hello **app per le API** blade, hello trova **API** sezione e quindi fare clic su **CORS**.</span><span class="sxs-lookup"><span data-stu-id="249ca-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Selezionare CORS nel portale](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="249ca-184">Nella casella di testo hello, immettere l'URL hello per l'app web di hello ToDoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="249ca-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="249ca-185">Ad esempio, se è stata distribuita denominato todolistangular0121 hello ToDoListAngular progetto tooa web app, consentire chiamate dall'URL hello `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="249ca-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="249ca-186">In alternativa, è possibile immettere toospecify un asterisco (*) che vengono accettati tutti i domini di origine.</span><span class="sxs-lookup"><span data-stu-id="249ca-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="249ca-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="249ca-187">Click **Save**.</span></span>
   
   ![Fare clic su Salva.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="249ca-189">Dopo aver fatto clic **salvare**, hello API app accetterà JavaScript chiamate da hello URL specificato.</span><span class="sxs-lookup"><span data-stu-id="249ca-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="249ca-190">In questa schermata, hello ToDoListAPI0223 API app accetterà le chiamate client JavaScript da hello ToDoListAngular web app.</span><span class="sxs-lookup"><span data-stu-id="249ca-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="249ca-191">Testare l'applicazione hello con CORS abilitato</span><span class="sxs-lookup"><span data-stu-id="249ca-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="249ca-192">Aprire un toohello browser URL HTTPS dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="249ca-193">Questa applicazione hello ora consente di visualizzare, aggiungere, modificare ed eliminare gli elementi di attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="249ca-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![pagina di elenco tooDo di app di esempio](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="249ca-195">CORS del servizio app e CORS di API Web</span><span class="sxs-lookup"><span data-stu-id="249ca-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="249ca-196">In un progetto di API Web, è possibile installare hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify pacchetto NuGet i domini che verranno accettate dall'API JavaScript chiamate dal codice.</span><span class="sxs-lookup"><span data-stu-id="249ca-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="249ca-197">Il supporto di CORS per l'API Web è più flessibile del supporto di CORS per il servizio app.</span><span class="sxs-lookup"><span data-stu-id="249ca-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="249ca-198">Ad esempio, nel codice è possibile specificare origini accettate diverse a seconda del metodo di azione, mentre per CORS per il servizio app si specifica un set di origini accettate per tutti i metodi di un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="249ca-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="249ca-199">Non tentare toouse sia Web API CORS e la condivisione CORS di servizio App in un'applicazione API.</span><span class="sxs-lookup"><span data-stu-id="249ca-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="249ca-200">CORS per il servizio app avrà la precedenza e CORS per l'API Web non avrà effetto.</span><span class="sxs-lookup"><span data-stu-id="249ca-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="249ca-201">Ad esempio, se si abilita un dominio di origine nel servizio App e abilitare tutti i domini di origine nel codice API Web, Azure API app accetterà solo le chiamate da dominio hello specificato in Azure.</span><span class="sxs-lookup"><span data-stu-id="249ca-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="249ca-202">Come tooenable CORS nel codice API Web</span><span class="sxs-lookup"><span data-stu-id="249ca-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="249ca-203">Hello passaggi riepiloga processo hello per abilitare il supporto di Web API CORS.</span><span class="sxs-lookup"><span data-stu-id="249ca-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="249ca-204">Per altre informazioni, vedere l'articolo relativo all' [abilitazione della condivisione di richieste tra le origini nelle API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="249ca-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="249ca-205">In un progetto di API Web, installare hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="249ca-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="249ca-206">Includere un `config.EnableCors()` riga di codice hello **registrare** metodo hello **WebApiConfig** classe, come esempio hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="249ca-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="249ca-207">Nel controller di Web API, aggiungere un `using` istruzione per hello `System.Web.Http.Cors` dello spazio dei nomi e aggiungere hello `EnableCors` attributo toohello controller classe o tooindividual metodi di azione.</span><span class="sxs-lookup"><span data-stu-id="249ca-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="249ca-208">Nell'esempio seguente di hello, supporto CORS applica toohello intera controller.</span><span class="sxs-lookup"><span data-stu-id="249ca-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="249ca-209">Uso di Gestione API di Azure con le app per le API</span><span class="sxs-lookup"><span data-stu-id="249ca-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="249ca-210">Se si utilizza Gestione API di Azure con un'applicazione API, configurare CORS in Gestione API anziché in app per le API hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="249ca-211">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="249ca-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="249ca-212">Panoramica di Gestione API di Azure (video: la sezione su CORS inizia al minuto 12:10)</span><span class="sxs-lookup"><span data-stu-id="249ca-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="249ca-213">Criteri tra domini di Gestione API</span><span class="sxs-lookup"><span data-stu-id="249ca-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="249ca-214">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="249ca-214">Troubleshooting</span></span>
<span data-ttu-id="249ca-215">In caso di problemi nel corso dell'esercitazione, ecco alcune idee per risolverli.</span><span class="sxs-lookup"><span data-stu-id="249ca-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="249ca-216">Assicurarsi che si usi l'ultima versione di hello di hello [Azure SDK per .NET per Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="249ca-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="249ca-217">Assicurarsi di avere immesso `https` in hello impostazione CORS e assicurarsi che si usi `https` toorun hello front-end web app.</span><span class="sxs-lookup"><span data-stu-id="249ca-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="249ca-218">Assicurarsi di avere immesso impostazione CORS hello in app hello per le API livello intermedio, non nell'applicazione web front-end hello.</span><span class="sxs-lookup"><span data-stu-id="249ca-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="249ca-219">Se si configura la condivisione CORS nel codice dell'applicazione e servizio App di Azure, si noti che impostazione CORS del servizio App hello sostituiranno qualsiasi eseguite nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="249ca-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="249ca-220">toolearn sulle funzionalità di Visual Studio che semplificano la risoluzione dei problemi, vedere [app di risoluzione dei problemi di servizio App di Azure in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="249ca-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="249ca-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="249ca-221">Next steps</span></span>
<span data-ttu-id="249ca-222">In questo articolo, si è visto come tooenable CORS del servizio App supportano in modo che il codice JavaScript client può chiamare un'API in un dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="249ca-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="249ca-223">altre informazioni sulle App per le API, leggere hello toolearn [tooauthentication introduzione nel servizio App](../app-service/app-service-authentication-overview.md), quindi andare toohello [l'autenticazione utente per App per le API](app-service-api-dotnet-user-principal-auth.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="249ca-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

