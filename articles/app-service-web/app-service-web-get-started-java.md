---
title: Creare la prima app Web Java in Azure
description: Informazioni su come eseguire app Web nel servizio app mediante la distribuzione di un'app Java di base.
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="bab35-103">Creare la prima app Web Java in Azure</span><span class="sxs-lookup"><span data-stu-id="bab35-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="bab35-104">La funzionalità [app Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) del [servizio app di Azure](../app-service/app-service-value-prop-what-is.md) fornisce un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="bab35-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="bab35-105">Questa guida introduttiva illustra come distribuire un'app Web Java nel servizio app usando [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="bab35-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![App Web di esempio "Hello Azure"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="bab35-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bab35-108">Prerequisites</span></span>

<span data-ttu-id="bab35-109">Per completare questa guida introduttiva, installare:</span><span class="sxs-lookup"><span data-stu-id="bab35-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="bab35-110">Lo strumento gratuito [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bab35-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="bab35-111">In questa guida introduttiva viene usato Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="bab35-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="bab35-112">[Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="bab35-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="bab35-113">Creare un progetto Web dinamico in Eclipse</span><span class="sxs-lookup"><span data-stu-id="bab35-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="bab35-114">In Eclipse selezionare **File** > **Nuovo** > **Dynamic Web Project** (Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="bab35-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="bab35-115">Nella finestra di dialogo **New Dynamic Web Project** (Nuovo progetto Web dinamico) assegnare al progetto il nome **MyFirstJavaOnAzureWebApp** e selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="bab35-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Finestra di dialogo New Dynamic Web Project (Nuovo progetto Web dinamico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="bab35-117">Aggiungere una pagina JSP</span><span class="sxs-lookup"><span data-stu-id="bab35-117">Add a JSP page</span></span>

<span data-ttu-id="bab35-118">Se Esplora progetti non viene visualizzato, è necessario ripristinarlo.</span><span class="sxs-lookup"><span data-stu-id="bab35-118">If Project Explorer is not displayed, restore it.</span></span>

![Area di lavoro Java EE per Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="bab35-120">In Esplora progetti espandere il progetto **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="bab35-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="bab35-121">Fare doppio clic su **WebContent** e quindi selezionare **Nuovo** > **JSP File** (File JSP).</span><span class="sxs-lookup"><span data-stu-id="bab35-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu per un nuovo file JSP in Esplora progetti](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="bab35-123">Nella finestra di dialogo **New JSP File** (Nuovo file JSP):</span><span class="sxs-lookup"><span data-stu-id="bab35-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="bab35-124">Assegnare al file il nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="bab35-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="bab35-125">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="bab35-125">Select **Finish**.</span></span>

  ![Finestra di dialogo New JSP File (Nuovo file JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="bab35-127">Nel file index.jsp sostituire l'elemento `<body></body>` con il markup seguente:</span><span class="sxs-lookup"><span data-stu-id="bab35-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="bab35-128">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bab35-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="bab35-129">Pubblicare l'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="bab35-129">Publish the web app to Azure</span></span>

<span data-ttu-id="bab35-130">In Esplora progetti fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Azure** > **Publish as Azure Web App** (Pubblica come app Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="bab35-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu di scelta rapida Publish as Azure Web App (Pubblica come app Web di Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="bab35-132">Nella finestra di dialogo **Accesso ad Azure** mantenere selezionata l'opzione **Interattivo** opzione e quindi selezionare **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="bab35-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="bab35-133">Seguire le istruzioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="bab35-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="bab35-134">Finestra di dialogo Distribuisci app Web</span><span class="sxs-lookup"><span data-stu-id="bab35-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="bab35-135">Dopo avere effettuato l'accesso all'account Azure, verrà visualizzata la finestra di dialogo **Distribuisci app Web**.</span><span class="sxs-lookup"><span data-stu-id="bab35-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="bab35-136">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bab35-136">Select **Create**.</span></span>

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="bab35-138">Finestra di dialogo Crea servizio app</span><span class="sxs-lookup"><span data-stu-id="bab35-138">Create App Service dialog box</span></span>

<span data-ttu-id="bab35-139">Viene visualizzata la finestra di dialogo **Crea servizio app** con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="bab35-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="bab35-140">Il numero **170602185241** illustrato nell'immagine seguente è diverso da quello visualizzato nella finestra di dialogo reale.</span><span class="sxs-lookup"><span data-stu-id="bab35-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="bab35-142">Nella finestra di dialogo **Crea servizio app**:</span><span class="sxs-lookup"><span data-stu-id="bab35-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="bab35-143">Lasciare invariato il nome generato per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="bab35-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="bab35-144">Il nome deve essere univoco in Azure</span><span class="sxs-lookup"><span data-stu-id="bab35-144">This name must be unique across Azure.</span></span> <span data-ttu-id="bab35-145">ed è incluso nell'indirizzo URL relativo all'app Web.</span><span class="sxs-lookup"><span data-stu-id="bab35-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="bab35-146">Se, ad esempio, il nome dell'app Web è **MyJavaWebApp**, l'URL è *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="bab35-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="bab35-147">Mantenere il contenitore Web predefinito.</span><span class="sxs-lookup"><span data-stu-id="bab35-147">Keep the default web container.</span></span>
* <span data-ttu-id="bab35-148">Selezionare una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bab35-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="bab35-149">Nella scheda **Piano di servizio app**:</span><span class="sxs-lookup"><span data-stu-id="bab35-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="bab35-150">**Crea nuovo**: mantenere il valore predefinito, ovvero il nome del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="bab35-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="bab35-151">**Località**: selezionare **Europa occidentale** o un'area geografica nelle vicinanze.</span><span class="sxs-lookup"><span data-stu-id="bab35-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="bab35-152">**Piano tariffario**: selezionare l'opzione gratuita.</span><span class="sxs-lookup"><span data-stu-id="bab35-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="bab35-153">Per le funzionalità, vedere [Prezzi di Servizio app](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="bab35-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="bab35-155">Scheda Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="bab35-155">Resource group tab</span></span>

<span data-ttu-id="bab35-156">Selezionare la scheda **Gruppo di risorse**. Mantenere il valore predefinito generato per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bab35-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Scheda Gruppo di risorse](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="bab35-158">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bab35-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="bab35-159">Azure Toolkit crea l'app Web e visualizza una finestra di dialogo di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="bab35-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Finestra di dialogo di avanzamento Crea servizio app](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="bab35-161">Finestra di dialogo Distribuisci app Web</span><span class="sxs-lookup"><span data-stu-id="bab35-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="bab35-162">Nella finestra di dialogo **Distribuisci app Web** selezionare **Deploy to root** (Distribuisci nella radice).</span><span class="sxs-lookup"><span data-stu-id="bab35-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="bab35-163">Se si ha un servizio app all'indirizzo *wingtiptoys.azurewebsites.net* e non si esegue la distribuzione nella radice, l'app Web denominata **MyFirstJavaOnAzureWebApp** verrà distribuita in *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="bab35-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="bab35-165">Nella finestra di dialogo vengono visualizzate le selezioni del contenitore Web, di Azure e di JDK.</span><span class="sxs-lookup"><span data-stu-id="bab35-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="bab35-166">Selezionare **Distribuisci** per pubblicare l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="bab35-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="bab35-167">Al termine del processo di pubblicazione, selezionare il collegamento **Pubblicato** nella finestra di dialogo **Log attività di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bab35-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Finestra di dialogo Log attività di Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="bab35-169">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="bab35-169">Congratulations!</span></span> <span data-ttu-id="bab35-170">L'app Web è stata distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="bab35-170">You have successfully deployed your web app to Azure.</span></span> 

![App Web di esempio "Hello Azure"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="bab35-173">Aggiornare l'app Web</span><span class="sxs-lookup"><span data-stu-id="bab35-173">Update the web app</span></span>

<span data-ttu-id="bab35-174">Modificare il codice JSP di esempio in un messaggio diverso.</span><span class="sxs-lookup"><span data-stu-id="bab35-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="bab35-175">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bab35-175">Save the changes.</span></span>

<span data-ttu-id="bab35-176">In Esplora progetti fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Azure** > **Publish as Azure Web App** (Pubblica come app Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="bab35-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="bab35-177">Viene visualizzata la finestra di dialogo **Distribuisci app Web** in cui viene illustrato il servizio app creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bab35-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="bab35-178">Selezionare **Deploy to root** (Distribuisci nella radice) ogni volta che si esegue una pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="bab35-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="bab35-179">Selezionare l'app Web e fare clic su **Distribuisci** per pubblicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bab35-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="bab35-180">Quando viene visualizzato il collegamento **Pubblicazione**, selezionarlo per passare all'app Web e visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bab35-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="bab35-181">Gestire l'app Web</span><span class="sxs-lookup"><span data-stu-id="bab35-181">Manage the web app</span></span>

<span data-ttu-id="bab35-182">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per visualizzare l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="bab35-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="bab35-183">Nel menu di sinistra selezionare **Gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="bab35-183">From the left menu, select **Resource Groups**.</span></span>

![Accesso ai gruppi di risorse nel portale](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="bab35-185">Selezionare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bab35-185">Select the resource group.</span></span> <span data-ttu-id="bab35-186">Nella pagina vengono visualizzate le risorse create in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="bab35-186">The page shows the resources that you created in this quickstart.</span></span>

![Gruppo di risorse myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="bab35-188">Selezionare l'app Web (**webapp 170602193915** nell'immagine precedente).</span><span class="sxs-lookup"><span data-stu-id="bab35-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="bab35-189">Viene visualizzata la pagina **Panoramica**,</span><span class="sxs-lookup"><span data-stu-id="bab35-189">The **Overview** page appears.</span></span> <span data-ttu-id="bab35-190">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="bab35-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="bab35-191">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="bab35-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="bab35-192">Le schede sul lato sinistro della pagina mostrano le diverse configurazioni che è possibile aprire.</span><span class="sxs-lookup"><span data-stu-id="bab35-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Pagina del servizio app nel portale di Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="bab35-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bab35-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bab35-195">Eseguire il mapping di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="bab35-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
