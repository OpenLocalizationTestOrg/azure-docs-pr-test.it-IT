---
title: aaaCreate della prima applicazione web Java in Azure
description: Informazioni su come toorun app nel servizio App web tramite la distribuzione di un'applicazione Java di base.
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
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="a38c9-103">Creare la prima app Web Java in Azure</span><span class="sxs-lookup"><span data-stu-id="a38c9-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="a38c9-104">Hello [App Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funzionalità di [Azure App Service](../app-service/app-service-value-prop-what-is.md) fornisce un servizio di hosting web scalabile, applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="a38c9-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a38c9-105">Questa Guida introduttiva viene illustrato come un linguaggio toodeploy web app tooApp servizio utilizzando hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="a38c9-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![App Web di esempio "Hello Azure"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="a38c9-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a38c9-108">Prerequisites</span></span>

<span data-ttu-id="a38c9-109">toocomplete questa Guida rapida, installare:</span><span class="sxs-lookup"><span data-stu-id="a38c9-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="a38c9-110">Hello libero [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a38c9-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="a38c9-111">In questa guida introduttiva viene usato Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="a38c9-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="a38c9-112">Hello [Azure Toolkit per Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="a38c9-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="a38c9-113">Creare un progetto Web dinamico in Eclipse</span><span class="sxs-lookup"><span data-stu-id="a38c9-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="a38c9-114">In Eclipse selezionare **File** > **Nuovo** > **Dynamic Web Project** (Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="a38c9-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="a38c9-115">In hello **nuovo progetto Web dinamico** della finestra di dialogo progetto hello nome **MyFirstJavaOnAzureWebApp**e selezionare **fine**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Finestra di dialogo New Dynamic Web Project (Nuovo progetto Web dinamico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="a38c9-117">Aggiungere una pagina JSP</span><span class="sxs-lookup"><span data-stu-id="a38c9-117">Add a JSP page</span></span>

<span data-ttu-id="a38c9-118">Se Esplora progetti non viene visualizzato, è necessario ripristinarlo.</span><span class="sxs-lookup"><span data-stu-id="a38c9-118">If Project Explorer is not displayed, restore it.</span></span>

![Area di lavoro Java EE per Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="a38c9-120">In Esplora progetti espandere hello **MyFirstJavaOnAzureWebApp** progetto.</span><span class="sxs-lookup"><span data-stu-id="a38c9-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="a38c9-121">Fare doppio clic su **WebContent** e quindi selezionare **Nuovo** > **JSP File** (File JSP).</span><span class="sxs-lookup"><span data-stu-id="a38c9-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu per un nuovo file JSP in Esplora progetti](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="a38c9-123">In hello **New JSP File** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="a38c9-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="a38c9-124">File con nome hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="a38c9-125">Selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-125">Select **Finish**.</span></span>

  ![Finestra di dialogo New JSP File (Nuovo file JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="a38c9-127">Nel file index.jsp hello sostituire hello `<body></body>` elemento con hello markup seguente:</span><span class="sxs-lookup"><span data-stu-id="a38c9-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="a38c9-128">Salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="a38c9-129">Pubblicare hello web app tooAzure</span><span class="sxs-lookup"><span data-stu-id="a38c9-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="a38c9-130">In Esplora progetti, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come App Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu di scelta rapida Publish as Azure Web App (Pubblica come app Web di Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="a38c9-132">In hello **Azure Accedi** della finestra di dialogo keep hello **Interactive** opzione e quindi selezionare **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="a38c9-133">Istruzioni hello Accedi.</span><span class="sxs-lookup"><span data-stu-id="a38c9-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="a38c9-134">Finestra di dialogo Distribuisci app Web</span><span class="sxs-lookup"><span data-stu-id="a38c9-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="a38c9-135">Dopo avere effettuato l'accesso in tooyour account Azure, hello **distribuire App Web** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a38c9-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="a38c9-136">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-136">Select **Create**.</span></span>

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="a38c9-138">Finestra di dialogo Crea servizio app</span><span class="sxs-lookup"><span data-stu-id="a38c9-138">Create App Service dialog box</span></span>

<span data-ttu-id="a38c9-139">Hello **Crea servizio App** viene visualizzata la finestra di dialogo con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="a38c9-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="a38c9-140">numero di Hello **170602185241** illustrato nella seguente hello immagine è diversa nella finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a38c9-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="a38c9-142">In hello **Crea servizio App** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="a38c9-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="a38c9-143">Mantenere il nome di hello generato per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="a38c9-144">Il nome deve essere univoco in Azure</span><span class="sxs-lookup"><span data-stu-id="a38c9-144">This name must be unique across Azure.</span></span> <span data-ttu-id="a38c9-145">nome Hello è parte dell'indirizzo URL hello hello web app.</span><span class="sxs-lookup"><span data-stu-id="a38c9-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="a38c9-146">Ad esempio: se il nome dell'app web hello è **MyJavaWebApp**, hello URL *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="a38c9-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="a38c9-147">Mantenere contenitore web predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-147">Keep hello default web container.</span></span>
* <span data-ttu-id="a38c9-148">Selezionare una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a38c9-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="a38c9-149">In hello **piano di servizio App** scheda:</span><span class="sxs-lookup"><span data-stu-id="a38c9-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="a38c9-150">**Creare nuovi**: mantenere il valore predefinito hello, ovvero nome hello del piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="a38c9-151">**Località**: selezionare **Europa occidentale** o un'area geografica nelle vicinanze.</span><span class="sxs-lookup"><span data-stu-id="a38c9-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="a38c9-152">**Piano tariffario**: selezionare hello opzione disponibile.</span><span class="sxs-lookup"><span data-stu-id="a38c9-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="a38c9-153">Per le funzionalità, vedere [Prezzi di Servizio app](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a38c9-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="a38c9-155">Scheda Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a38c9-155">Resource group tab</span></span>

<span data-ttu-id="a38c9-156">Seleziona hello **gruppo di risorse** scheda. Mantenere il valore predefinito generato hello per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Scheda Gruppo di risorse](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="a38c9-158">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="a38c9-159">Hello Azure Toolkit crea app web hello e visualizza una finestra di dialogo di stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="a38c9-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Finestra di dialogo di avanzamento Crea servizio app](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="a38c9-161">Finestra di dialogo Distribuisci app Web</span><span class="sxs-lookup"><span data-stu-id="a38c9-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="a38c9-162">In hello **distribuire App Web** nella finestra di dialogo **distribuire tooroot**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="a38c9-163">Se si dispone di un servizio app *wingtiptoys.azurewebsites.net* e non si distribuisce toohello radice, app web hello denominata **MyFirstJavaOnAzureWebApp** viene distribuito troppo *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="a38c9-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="a38c9-165">Hello della finestra di dialogo Mostra hello Azure JDK e le selezioni di contenitore di web.</span><span class="sxs-lookup"><span data-stu-id="a38c9-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="a38c9-166">Selezionare **Distribuisci** toopublish hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a38c9-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="a38c9-167">Al termine della pubblicazione hello, selezionare hello **pubblicato** collegamento hello **Log attività Azure** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a38c9-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Finestra di dialogo Log attività di Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="a38c9-169">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a38c9-169">Congratulations!</span></span> <span data-ttu-id="a38c9-170">È stata distribuita la tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="a38c9-170">You have successfully deployed your web app tooAzure.</span></span> 

![App Web di esempio "Hello Azure"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="a38c9-173">Aggiornare l'app web hello</span><span class="sxs-lookup"><span data-stu-id="a38c9-173">Update hello web app</span></span>

<span data-ttu-id="a38c9-174">Modifica hello esempio JSP codice tooa messaggi diversi.</span><span class="sxs-lookup"><span data-stu-id="a38c9-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="a38c9-175">Salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-175">Save hello changes.</span></span>

<span data-ttu-id="a38c9-176">In Esplora progetti, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come App Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="a38c9-177">Hello **distribuire App Web** viene visualizzata la finestra di dialogo e Mostra hello servizio app creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a38c9-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="a38c9-178">Selezionare **distribuire tooroot** ogni volta che si esegue la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a38c9-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="a38c9-179">Selezionare l'app web hello e selezionare **Distribuisci**, che vengono pubblicate modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="a38c9-180">Quando hello **pubblicazione** collegamento viene visualizzato, selezionarlo toobrowse toohello web app e visualizzare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="a38c9-181">Gestire app web hello</span><span class="sxs-lookup"><span data-stu-id="a38c9-181">Manage hello web app</span></span>

<span data-ttu-id="a38c9-182">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toosee hello web app a cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a38c9-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="a38c9-183">Scegliere dal menu a sinistra hello **gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="a38c9-183">From hello left menu, select **Resource Groups**.</span></span>

![Gruppi di navigazione del portale tooresource](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="a38c9-185">Selezionare il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-185">Select hello resource group.</span></span> <span data-ttu-id="a38c9-186">pagina Hello Mostra risorse hello creati in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="a38c9-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Gruppo di risorse myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="a38c9-188">Selezionare hello web app (**webapp 170602193915** in hello prima immagine).</span><span class="sxs-lookup"><span data-stu-id="a38c9-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="a38c9-189">Hello **Panoramica** verrà visualizzata la pagina.</span><span class="sxs-lookup"><span data-stu-id="a38c9-189">hello **Overview** page appears.</span></span> <span data-ttu-id="a38c9-190">Questa pagina offre una visualizzazione di svolgimento app hello.</span><span class="sxs-lookup"><span data-stu-id="a38c9-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="a38c9-191">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a38c9-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a38c9-192">schede di Hello sul lato sinistro di hello della pagina hello mostrano hello diverse configurazioni che è possibile aprire.</span><span class="sxs-lookup"><span data-stu-id="a38c9-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Pagina del servizio app nel portale di Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="a38c9-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a38c9-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a38c9-195">Eseguire il mapping di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="a38c9-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
