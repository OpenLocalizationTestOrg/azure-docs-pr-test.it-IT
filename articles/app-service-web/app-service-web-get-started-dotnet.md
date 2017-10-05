---
title: Creare un'app Web ASP.NET in Azure | Microsoft Docs
description: Informazioni su come eseguire app Web nel servizio app di Azure distribuendo l'app Web ASP.NET predefinita.
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
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="6cd04-103">Creare un'app Web ASP.NET in Azure</span><span class="sxs-lookup"><span data-stu-id="6cd04-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="6cd04-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="6cd04-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="6cd04-105">Questa guida introduttiva illustra come distribuire la prima app Web ASP.NET in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="6cd04-106">Al termine della procedura si avrà un gruppo di risorse costituito da un piano di servizio App e da un'app Web di Azure con un'applicazione Web distribuita.</span><span class="sxs-lookup"><span data-stu-id="6cd04-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="6cd04-107">Guardare il video per osservare il funzionamento di questa guida introduttiva e quindi seguire personalmente la procedura per pubblicare la prima app .NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="6cd04-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6cd04-108">Prerequisites</span></span>

<span data-ttu-id="6cd04-109">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="6cd04-109">To complete this tutorial:</span></span>

* <span data-ttu-id="6cd04-110">Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con i carichi di lavoro seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cd04-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="6cd04-111">**Sviluppo Web e ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="6cd04-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="6cd04-112">**Sviluppo di Azure**</span><span class="sxs-lookup"><span data-stu-id="6cd04-112">**Azure development**</span></span>

    ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="6cd04-114">Creare un'app Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6cd04-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="6cd04-115">In Visual Studio creare un progetto selezionando **File > Nuovo > Progetto**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="6cd04-116">Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C# > Web > Applicazione Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="6cd04-117">Assegnare all'applicazione il nome _myFirstAzureWebApp_ e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Finestra di dialogo Nuovo progetto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="6cd04-119">È possibile distribuire qualsiasi tipo di app Web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="6cd04-120">Per questa guida introduttiva, selezionare il modello **MVC** e verificare che l'autenticazione sia impostata su **Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="6cd04-121">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-121">Select **OK**.</span></span>

![Finestra di dialogo Nuovo progetto ASP.NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="6cd04-123">Nel menu selezionare **Debug > Avvia senza eseguire debug** per eseguire l'app Web in locale.</span><span class="sxs-lookup"><span data-stu-id="6cd04-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Eseguire l'app in locale](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="6cd04-125">Pubblicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="6cd04-125">Publish to Azure</span></span>

<span data-ttu-id="6cd04-126">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **myFirstAzureWebApp** e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Pubblicare da Esplora soluzioni](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="6cd04-128">Verificare che **Servizio app di Microsoft Azure** sia selezionato e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="6cd04-130">Viene visualizzata la finestra di dialogo **Crea servizio app**, che consente di creare tutte le risorse di Azure necessarie per eseguire l'app Web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="6cd04-131">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="6cd04-131">Sign in to Azure</span></span>

<span data-ttu-id="6cd04-132">Nella finestra di dialogo **Crea servizio app** fare clic su **Aggiungi un account** e accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="6cd04-133">Se è già stato eseguito l'accesso, selezionare l'account contenente la sottoscrizione desiderata dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="6cd04-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="6cd04-134">Se si è già connessi, non selezionare ancora l'opzione **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Accedere ad Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="6cd04-136">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="6cd04-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="6cd04-137">Accanto a **Gruppo di risorse** selezionare **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="6cd04-138">Assegnare al gruppo di risorse il nome **myResourceGroup** e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="6cd04-139">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6cd04-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="6cd04-140">Accanto a **Piano di servizio app** selezionare **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="6cd04-141">Nella finestra di dialogo **Configura piano di servizio app** usare le impostazioni della tabella riportata sotto l'immagine.</span><span class="sxs-lookup"><span data-stu-id="6cd04-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Creare un piano di servizio app](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="6cd04-143">Impostazione</span><span class="sxs-lookup"><span data-stu-id="6cd04-143">Setting</span></span> | <span data-ttu-id="6cd04-144">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="6cd04-144">Suggested Value</span></span> | <span data-ttu-id="6cd04-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cd04-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="6cd04-146">Piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6cd04-146">App Service Plan</span></span>| <span data-ttu-id="6cd04-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6cd04-147">myAppServicePlan</span></span> | <span data-ttu-id="6cd04-148">Nome del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6cd04-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="6cd04-149">Località</span><span class="sxs-lookup"><span data-stu-id="6cd04-149">Location</span></span> | <span data-ttu-id="6cd04-150">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="6cd04-150">West Europe</span></span> | <span data-ttu-id="6cd04-151">Data center in cui è ospitata l'app Web.</span><span class="sxs-lookup"><span data-stu-id="6cd04-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="6cd04-152">Dimensione</span><span class="sxs-lookup"><span data-stu-id="6cd04-152">Size</span></span> | <span data-ttu-id="6cd04-153">Gratuito</span><span class="sxs-lookup"><span data-stu-id="6cd04-153">Free</span></span> | <span data-ttu-id="6cd04-154">[Piano tariffario](https://azure.microsoft.com/pricing/details/app-service/) che determina le funzionalità di hosting.</span><span class="sxs-lookup"><span data-stu-id="6cd04-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="6cd04-155">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="6cd04-156">Creare e pubblicare l'app Web</span><span class="sxs-lookup"><span data-stu-id="6cd04-156">Create and publish the web app</span></span>

<span data-ttu-id="6cd04-157">In **Nome app Web** immettere un nome univoco dell'app, usando i caratteri validi `a-z`, `0-9` e `-`, o accettare il nome univoco generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6cd04-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="6cd04-158">L'URL dell'app Web è `http://<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6cd04-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="6cd04-159">Selezionare **Crea** per avviare la creazione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-159">Select **Create** to start creating the Azure resources.</span></span>

![Configurare il nome dell'app Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="6cd04-161">Al termine della procedura guidata, l'app Web ASP.NET viene pubblicata in Azure e avviata nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="6cd04-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![App Web ASP.NET pubblicata in Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="6cd04-163">Il nome dell'app Web specificato nel passaggio relativo alla [creazione e pubblicazione](#create-and-publish-the-web-app) viene usato come prefisso dell'URL nel formato `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="6cd04-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="6cd04-164">L'app Web ASP.NET è ora in esecuzione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="6cd04-165">Aggiornare e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="6cd04-165">Update the app and redeploy</span></span>

<span data-ttu-id="6cd04-166">Da **Esplora soluzioni** aprire _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="6cd04-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="6cd04-167">Trovare il tag HTML `<div class="jumbotron">` in alto e sostituire l'intero elemento con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="6cd04-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="6cd04-168">Per la ridistribuzione in Azure, fare clic con il pulsante destro del mouse sul progetto **myFirstAzureWebApp** in **Esplora soluzioni** e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="6cd04-169">Nella pagina di pubblicazione selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="6cd04-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="6cd04-170">Al termine del processo di pubblicazione, Visual Studio avvia un browser sull'URL dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6cd04-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![App Web ASP.NET aggiornata in Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="6cd04-172">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="6cd04-172">Manage the Azure web app</span></span>

<span data-ttu-id="6cd04-173">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per visualizzare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="6cd04-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="6cd04-174">Scegliere **Servizi app** dal menu a sinistra e quindi selezionare il nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cd04-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="6cd04-176">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6cd04-176">You see your web app's Overview page.</span></span> <span data-ttu-id="6cd04-177">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6cd04-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="6cd04-179">Il menu a sinistra fornisce varie pagine per la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6cd04-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="6cd04-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cd04-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cd04-181">ASP.NET con database SQL</span><span class="sxs-lookup"><span data-stu-id="6cd04-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
