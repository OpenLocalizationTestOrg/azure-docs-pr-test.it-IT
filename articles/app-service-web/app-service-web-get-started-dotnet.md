---
title: aaaCreate ASP.NET web app in Azure | Documenti Microsoft
description: Informazioni su come le app web di toorun distribuendo predefinito hello ASP.NET in Azure App Service app web.
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="c2ccc-103">Creare un'app Web ASP.NET in Azure</span><span class="sxs-lookup"><span data-stu-id="c2ccc-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="c2ccc-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="c2ccc-105">Questa Guida introduttiva viene illustrato come toodeploy prima ASP.NET web app tooAzure App Web.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="c2ccc-106">Al termine della procedura si avrà un gruppo di risorse costituito da un piano di servizio App e da un'app Web di Azure con un'applicazione Web distribuita.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="c2ccc-107">Guardare video toosee di hello questa Guida introduttiva nell'azione e quindi seguire hello passaggi manualmente toopublish della prima applicazione .NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="c2ccc-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c2ccc-108">Prerequisites</span></span>

<span data-ttu-id="c2ccc-109">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="c2ccc-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="c2ccc-110">Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello carichi di lavoro seguente:</span><span class="sxs-lookup"><span data-stu-id="c2ccc-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="c2ccc-111">**Sviluppo Web e ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="c2ccc-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="c2ccc-112">**Sviluppo di Azure**</span><span class="sxs-lookup"><span data-stu-id="c2ccc-112">**Azure development**</span></span>

    ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="c2ccc-114">Creare un'app Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c2ccc-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="c2ccc-115">In Visual Studio creare un progetto selezionando **File > Nuovo > Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="c2ccc-116">In hello **nuovo progetto** finestra di dialogo Seleziona **Visual c# > Web > applicazione Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="c2ccc-117">Nome di un'applicazione hello _myFirstAzureWebApp_, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Finestra di dialogo Nuovo progetto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="c2ccc-119">È possibile distribuire qualsiasi tipo di tooAzure di app web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="c2ccc-120">Per questa Guida rapida, selezionare hello **MVC** , modello e assicurarsi che l'autenticazione è impostata troppo**Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="c2ccc-121">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-121">Select **OK**.</span></span>

![Finestra di dialogo Nuovo progetto ASP.NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="c2ccc-123">Scegliere dal menu hello **Debug > Avvia senza eseguire debug** toorun hello web app localmente.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Eseguire l'app in locale](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="c2ccc-125">Pubblicare tooAzure</span><span class="sxs-lookup"><span data-stu-id="c2ccc-125">Publish tooAzure</span></span>

<span data-ttu-id="c2ccc-126">In hello **Esplora**, hello rapida **myFirstAzureWebApp** del progetto e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Pubblicare da Esplora soluzioni](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="c2ccc-128">Verificare che **Servizio app di Microsoft Azure** sia selezionato e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="c2ccc-130">Verrà visualizzata hello **Crea servizio App** finestra di dialogo che consente di creare tutti hello necessarie risorse di Azure toorun hello app web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="c2ccc-131">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="c2ccc-131">Sign in tooAzure</span></span>

<span data-ttu-id="c2ccc-132">In hello **Crea servizio App** finestra di dialogo Seleziona **aggiungere un account**ed eseguire l'accesso tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="c2ccc-133">Se hai già effettuato l'accesso, account selezionare hello contenente hello desiderato sottoscrizione dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ccc-134">Se si è già connessi, non selezionare ancora l'opzione **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Accedi tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="c2ccc-136">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c2ccc-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="c2ccc-137">Avanti troppo**gruppo di risorse**selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="c2ccc-138">Nome gruppo di risorse hello **myResourceGroup** e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="c2ccc-139">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="c2ccc-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="c2ccc-140">Avanti troppo**piano di servizio App**selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="c2ccc-141">In hello **configurare il piano di servizio App** finestra di dialogo, utilizza le impostazioni di hello nella tabella hello hello schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Creare un piano di servizio app](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="c2ccc-143">Impostazione</span><span class="sxs-lookup"><span data-stu-id="c2ccc-143">Setting</span></span> | <span data-ttu-id="c2ccc-144">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="c2ccc-144">Suggested Value</span></span> | <span data-ttu-id="c2ccc-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c2ccc-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="c2ccc-146">Piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="c2ccc-146">App Service Plan</span></span>| <span data-ttu-id="c2ccc-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c2ccc-147">myAppServicePlan</span></span> | <span data-ttu-id="c2ccc-148">Nome del piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="c2ccc-149">Percorso</span><span class="sxs-lookup"><span data-stu-id="c2ccc-149">Location</span></span> | <span data-ttu-id="c2ccc-150">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="c2ccc-150">West Europe</span></span> | <span data-ttu-id="c2ccc-151">Hello Data Center in cui è ospitato app web hello.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="c2ccc-152">Dimensione</span><span class="sxs-lookup"><span data-stu-id="c2ccc-152">Size</span></span> | <span data-ttu-id="c2ccc-153">Gratuito</span><span class="sxs-lookup"><span data-stu-id="c2ccc-153">Free</span></span> | <span data-ttu-id="c2ccc-154">[Piano tariffario](https://azure.microsoft.com/pricing/details/app-service/) che determina le funzionalità di hosting.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="c2ccc-155">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="c2ccc-156">Creare e pubblicare app web hello</span><span class="sxs-lookup"><span data-stu-id="c2ccc-156">Create and publish hello web app</span></span>

<span data-ttu-id="c2ccc-157">In **nome dell'applicazione Web**, digitare un nome univoco dell'app (i caratteri validi sono `a-z`, `0-9`, e `-`), o accettare hello generato automaticamente un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="c2ccc-158">l'URL dell'app web hello Hello è `http://<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="c2ccc-159">Selezionare **crea** toostart creazione hello risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Configurare il nome dell'app Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="c2ccc-161">Una volta completata la procedura guidata hello, pubblica tooAzure di app web ASP.NET hello e quindi avvia hello app nel browser predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![App Web ASP.NET pubblicata in Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="c2ccc-163">nome dell'applicazione web Hello specificato in hello [creare e pubblicare passaggio](#create-and-publish-the-web-app) viene utilizzato come prefisso di URL in formato hello hello `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="c2ccc-164">L'app Web ASP.NET è ora in esecuzione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="c2ccc-165">Ridistribuzione e l'applicazione hello aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c2ccc-165">Update hello app and redeploy</span></span>

<span data-ttu-id="c2ccc-166">Da hello **Esplora**aprire _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="c2ccc-167">Trovare hello `<div class="jumbotron">` HTML tag superiore hello e sostituire l'intero elemento hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="c2ccc-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="c2ccc-168">tooredeploy tooAzure, hello rapida **myFirstAzureWebApp** nel progetto **Esplora** e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="c2ccc-169">Pagina pubblica hello, selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="c2ccc-170">Al termine del processo di pubblicazione, Visual Studio avvia un browser toohello URL hello web app.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![App Web ASP.NET aggiornata in Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="c2ccc-172">Gestire app web di Azure hello</span><span class="sxs-lookup"><span data-stu-id="c2ccc-172">Manage hello Azure web app</span></span>

<span data-ttu-id="c2ccc-173">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="c2ccc-174">Scegliere dal menu a sinistra hello **servizi App**, quindi selezionare il nome di hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="c2ccc-176">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-176">You see your web app's Overview page.</span></span> <span data-ttu-id="c2ccc-177">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="c2ccc-179">menu a sinistra di Hello fornisce diverse pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="c2ccc-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="c2ccc-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2ccc-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2ccc-181">ASP.NET con database SQL</span><span class="sxs-lookup"><span data-stu-id="c2ccc-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
