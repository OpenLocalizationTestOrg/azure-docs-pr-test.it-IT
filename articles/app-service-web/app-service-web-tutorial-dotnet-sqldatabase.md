---
title: Creare un'app ASP.NET in Azure con un database SQL | Microsoft Docs
description: "Informazioni su come ottenere un'app ASP.NET che è possibile usare in Azure con connessione a un database SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="eaf82-103">Creare un'app ASP.NET in Azure con un database SQL</span><span class="sxs-lookup"><span data-stu-id="eaf82-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="eaf82-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="eaf82-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="eaf82-105">Questa esercitazione illustra come distribuire un'app Web ASP.NET basata sui dati in Azure e connetterla al [database SQL di Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eaf82-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="eaf82-106">Al termine sarà disponibile un'applicazione ASP.NET in esecuzione nel [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) e connessa al database SQL.</span><span class="sxs-lookup"><span data-stu-id="eaf82-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="eaf82-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="eaf82-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaf82-109">Creare un database SQL in Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="eaf82-110">Connettere un'app ASP.NET al database SQL</span><span class="sxs-lookup"><span data-stu-id="eaf82-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="eaf82-111">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="eaf82-112">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="eaf82-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="eaf82-113">Eseguire lo streaming dei log da Azure al terminale</span><span class="sxs-lookup"><span data-stu-id="eaf82-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="eaf82-114">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eaf82-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eaf82-115">Prerequisites</span></span>

<span data-ttu-id="eaf82-116">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="eaf82-116">To complete this tutorial:</span></span>

* <span data-ttu-id="eaf82-117">Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con i carichi di lavoro seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaf82-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="eaf82-118">**Sviluppo Web e ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="eaf82-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="eaf82-119">**Sviluppo di Azure**</span><span class="sxs-lookup"><span data-stu-id="eaf82-119">**Azure development**</span></span>

  ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="eaf82-121">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="eaf82-121">Download the sample</span></span>

<span data-ttu-id="eaf82-122">[Scaricare il progetto di esempio](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="eaf82-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="eaf82-123">Estrarre (decomprimere) il file *dotnet-sqldb-tutorial-master.zip*.</span><span class="sxs-lookup"><span data-stu-id="eaf82-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="eaf82-124">Il progetto di esempio contiene un'app CRUD (create-read-update-delete) [ASP.NET MVC](https://www.asp.net/mvc) di base che usa [Code First di Entity Framework](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="eaf82-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="eaf82-125">Esecuzione dell'app</span><span class="sxs-lookup"><span data-stu-id="eaf82-125">Run the app</span></span>

<span data-ttu-id="eaf82-126">Aprire il file *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eaf82-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="eaf82-127">Digitare `Ctrl+F5` per eseguire l'app senza debug.</span><span class="sxs-lookup"><span data-stu-id="eaf82-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="eaf82-128">L'app viene visualizzata nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="eaf82-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="eaf82-129">Selezionare il collegamento **Crea nuovo** e creare due elementi *Attività*.</span><span class="sxs-lookup"><span data-stu-id="eaf82-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Finestra di dialogo Nuovo progetto ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="eaf82-131">Testare i collegamenti **Modifica**, **Dettagli** ed **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="eaf82-132">L'app usa un contesto di database per connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="eaf82-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="eaf82-133">Nell'esempio il contesto di database usa una stringa di connessione denominata `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="eaf82-134">La stringa di connessione è impostata nel file *Web.config* e il file *Models\MyDatabaseContext.cs* include un riferimento alla stringa.</span><span class="sxs-lookup"><span data-stu-id="eaf82-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="eaf82-135">Il nome della stringa di connessione è usato più avanti nell'esercitazione per connettere l'app Web di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="eaf82-136">Pubblicare in Azure con il database SQL</span><span class="sxs-lookup"><span data-stu-id="eaf82-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="eaf82-137">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **DotNetAppSqlDb** e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Pubblicare da Esplora soluzioni](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="eaf82-139">Verificare che **Servizio app di Microsoft Azure** sia selezionato e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="eaf82-141">La pubblicazione apre la finestra di dialogo **Crea servizio app** che consente di creare tutte le risorse di Azure necessarie per eseguire l'app Web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="eaf82-142">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-142">Sign in to Azure</span></span>

<span data-ttu-id="eaf82-143">Nella finestra di dialogo **Crea servizio App** fare clic su **Aggiungi un account** e quindi accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="eaf82-144">Se si è già connessi a un account Microsoft, verificare che l'account contenga la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="eaf82-145">Se l'account Microsoft a cui si è connessi non include la sottoscrizione di Azure, fare clic su di esso per aggiungere l'account corretto.</span><span class="sxs-lookup"><span data-stu-id="eaf82-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Accedere ad Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="eaf82-147">Dopo avere eseguito l'accesso, è possibile creare tutte le risorse necessarie per l'app Web di Azure in questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="eaf82-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="eaf82-148">Configurare il nome dell'app Web</span><span class="sxs-lookup"><span data-stu-id="eaf82-148">Configure the web app name</span></span>

<span data-ttu-id="eaf82-149">È possibile mantenere il nome dell'app Web generato o modificarlo in un altro nome univoco (i caratteri validi sono `a-z`, `0-9` e `-`).</span><span class="sxs-lookup"><span data-stu-id="eaf82-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="eaf82-150">Il nome dell'app Web viene usato come parte dell'URL predefinito per l'app (`<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'app Web).</span><span class="sxs-lookup"><span data-stu-id="eaf82-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="eaf82-151">Il nome dell'app Web deve essere univoco in tutte le app di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Finestra di dialogo Crea servizio app](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="eaf82-153">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="eaf82-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="eaf82-154">Accanto a **Gruppo di risorse** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-154">Next to **Resource Group**, click **New**.</span></span>

![Accanto a Gruppo di risorse fare clic su Nuovo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="eaf82-156">Assegnare al gruppo di risorse il nome **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf82-157">Non fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-157">Do not click **Create**.</span></span> <span data-ttu-id="eaf82-158">È prima necessario configurare un database SQL in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="eaf82-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="eaf82-159">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="eaf82-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="eaf82-160">Accanto a **Piano di servizio app** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="eaf82-161">Nella finestra di dialogo **Configura piano di servizio app** configurare il nuovo piano di servizio app con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaf82-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Creare un piano di servizio app](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="eaf82-163">Impostazione</span><span class="sxs-lookup"><span data-stu-id="eaf82-163">Setting</span></span>  | <span data-ttu-id="eaf82-164">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="eaf82-164">Suggested value</span></span> | <span data-ttu-id="eaf82-165">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="eaf82-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="eaf82-166">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="eaf82-166">**App Service Plan**</span></span>| <span data-ttu-id="eaf82-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="eaf82-167">myAppServicePlan</span></span> | [<span data-ttu-id="eaf82-168">Piani del servizio app</span><span class="sxs-lookup"><span data-stu-id="eaf82-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="eaf82-169">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="eaf82-169">**Location**</span></span>| <span data-ttu-id="eaf82-170">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="eaf82-170">West Europe</span></span> | [<span data-ttu-id="eaf82-171">Aree di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="eaf82-172">**Dimensione**</span><span class="sxs-lookup"><span data-stu-id="eaf82-172">**Size**</span></span>| <span data-ttu-id="eaf82-173">Free</span><span class="sxs-lookup"><span data-stu-id="eaf82-173">Free</span></span> | [<span data-ttu-id="eaf82-174">Piani tariffari</span><span class="sxs-lookup"><span data-stu-id="eaf82-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="eaf82-175">Creare un'istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="eaf82-175">Create a SQL Server instance</span></span>

<span data-ttu-id="eaf82-176">Prima di creare un database è necessario un [server logico di database SQL di Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="eaf82-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="eaf82-177">Un server logico contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="eaf82-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="eaf82-178">Selezionare **Esplora altri servizi di Azure**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-178">Select **Explore additional Azure services**.</span></span>

![Configurare il nome dell'app Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="eaf82-180">Nella scheda **Servizi** fare clic sull'icona **+** accanto a **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Nella scheda Servizi fare clic sull'icona + accanto a Database SQL.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="eaf82-182">nella finestra di dialogo **Configura database SQL** fare clic su **Nuovo** accanto a **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="eaf82-183">Viene generato un nome di server univoco.</span><span class="sxs-lookup"><span data-stu-id="eaf82-183">A unique server name is generated.</span></span> <span data-ttu-id="eaf82-184">Questo nome viene usato come parte dell'URL predefinito per il server logico `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="eaf82-185">Deve essere univoco in tutte le istanze di server logico in Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="eaf82-186">Sebbene sia possibile modificare il nome del server, per questa esercitazione mantenere il valore generato.</span><span class="sxs-lookup"><span data-stu-id="eaf82-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="eaf82-187">Aggiungere un nome utente e una password di amministratore e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="eaf82-188">Per i requisiti di complessità delle password, vedere [Criteri password](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="eaf82-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="eaf82-189">Prendere nota del nome utente e della password.</span><span class="sxs-lookup"><span data-stu-id="eaf82-189">Remember this username and password.</span></span> <span data-ttu-id="eaf82-190">Saranno necessari per gestire l'istanza del server logico in seguito.</span><span class="sxs-lookup"><span data-stu-id="eaf82-190">You need them to manage the logical server instance later.</span></span>

![Creare un'istanza di SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="eaf82-192">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="eaf82-192">Create a SQL Database</span></span>

<span data-ttu-id="eaf82-193">Nella finestra di dialogo **Configura database SQL**:</span><span class="sxs-lookup"><span data-stu-id="eaf82-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="eaf82-194">Mantenere il **Nome database** generato predefinito.</span><span class="sxs-lookup"><span data-stu-id="eaf82-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="eaf82-195">In **Nome stringa di connessione** digitare *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="eaf82-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="eaf82-196">Questo nome deve corrispondere alla stringa di connessione cui viene fatto riferimento in *Models\MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="eaf82-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="eaf82-197">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-197">Select **OK**.</span></span>

![Configurare il database SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="eaf82-199">La finestra di dialogo **Crea servizio app** mostra le risorse create.</span><span class="sxs-lookup"><span data-stu-id="eaf82-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="eaf82-200">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-200">Click **Create**.</span></span> 

![Risorse create](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="eaf82-202">Dopo aver creato le risorse di Azure, la procedura guidata pubblica l'app ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="eaf82-203">Il browser predefinito viene avviato con l'URL dell'app distribuita.</span><span class="sxs-lookup"><span data-stu-id="eaf82-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="eaf82-204">Aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="eaf82-204">Add a few to-do items.</span></span>

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="eaf82-206">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="eaf82-206">Congratulations!</span></span> <span data-ttu-id="eaf82-207">L'applicazione ASP.NET basata sui dati è in esecuzione nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="eaf82-208">Accedere al database SQL locale</span><span class="sxs-lookup"><span data-stu-id="eaf82-208">Access the SQL Database locally</span></span>

<span data-ttu-id="eaf82-209">Visual Studio consente di esplorare e gestire facilmente il nuovo database SQL in **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="eaf82-210">Creare una connessione al database</span><span class="sxs-lookup"><span data-stu-id="eaf82-210">Create a database connection</span></span>

<span data-ttu-id="eaf82-211">Dal menu **Visualizza** selezionare **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="eaf82-212">Nella parte superiore di **Esplora oggetti di SQL Server** fare clic sul pulsante **Aggiungi istanza di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="eaf82-213">Configurare la connessione al database</span><span class="sxs-lookup"><span data-stu-id="eaf82-213">Configure the database connection</span></span>

<span data-ttu-id="eaf82-214">Nella finestra di dialogo **Connetti** espandere il nodo **Azure**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="eaf82-215">Vengono visualizzate tutte le istanze del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="eaf82-216">Selezionare il database SQL `DotNetAppSqlDb`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="eaf82-217">La connessione creata in precedenza viene inserita automaticamente nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="eaf82-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="eaf82-218">Digitare la password di amministratore di database creata in precedenza e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Configurare la connessione al database da Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="eaf82-220">Consentire la connessione client dal computer</span><span class="sxs-lookup"><span data-stu-id="eaf82-220">Allow client connection from your computer</span></span>

<span data-ttu-id="eaf82-221">Viene visualizzata la finestra di dialogo **Crea nuova regola del firewall**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="eaf82-222">Per impostazione predefinita, l'istanza del database SQL consente solo le connessioni da servizi di Azure, ad esempio dall'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="eaf82-223">Per connettersi al database, creare una regola del firewall nell'istanza del database SQL.</span><span class="sxs-lookup"><span data-stu-id="eaf82-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="eaf82-224">La regola del firewall autorizza l'indirizzo IP pubblico del computer locale.</span><span class="sxs-lookup"><span data-stu-id="eaf82-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="eaf82-225">Nella finestra di dialogo è già specificato l'indirizzo IP pubblico del computer.</span><span class="sxs-lookup"><span data-stu-id="eaf82-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="eaf82-226">Assicurarsi che l'opzione **Aggiungi IP client** sia selezionata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Impostare il firewall per l'istanza del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="eaf82-228">Dopo che Visual Studio ha completato la creazione dell'impostazione del firewall per l'istanza del database SQL, la connessione viene visualizzata in **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="eaf82-229">In questa posizione è possibile eseguire le operazioni di database più comuni, ad esempio eseguire query, creare visualizzazioni e stored procedure e così via.</span><span class="sxs-lookup"><span data-stu-id="eaf82-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="eaf82-230">Fare clic con il pulsante destro del mouse sulla tabella `Todoes` e selezionare **Visualizza dati**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Esplorare gli oggetti del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="eaf82-232">Aggiornare l'app con Migrazioni Code First</span><span class="sxs-lookup"><span data-stu-id="eaf82-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="eaf82-233">Per aggiornare il database e l'app Web in Azure è possibile usare gli strumenti noti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eaf82-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="eaf82-234">In questo passaggio si usa Migrazioni Code First di Entity Framework per apportare una modifica allo schema del database e pubblicarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="eaf82-235">Per altre informazioni sull'uso di Migrazioni Code First di Entity Framework, vedere [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Introduzione a Code First di Entity Framework 6 con MVC 5).</span><span class="sxs-lookup"><span data-stu-id="eaf82-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="eaf82-236">Aggiornare il modello di dati</span><span class="sxs-lookup"><span data-stu-id="eaf82-236">Update your data model</span></span>

<span data-ttu-id="eaf82-237">Aprire _Models\Todo.cs_ nell'editor di codice.</span><span class="sxs-lookup"><span data-stu-id="eaf82-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="eaf82-238">Aggiungere la proprietà seguente alla classe `ToDo`:</span><span class="sxs-lookup"><span data-stu-id="eaf82-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="eaf82-239">Eseguire Migrazioni Code First in locale</span><span class="sxs-lookup"><span data-stu-id="eaf82-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="eaf82-240">Eseguire alcuni comandi per eseguire gli aggiornamenti del database locale.</span><span class="sxs-lookup"><span data-stu-id="eaf82-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="eaf82-241">Nel menu **Strumenti** fare clic su **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="eaf82-242">Nella finestra Console di Gestione pacchetti abilitare le migrazioni Code First:</span><span class="sxs-lookup"><span data-stu-id="eaf82-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="eaf82-243">Aggiungere una migrazione:</span><span class="sxs-lookup"><span data-stu-id="eaf82-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="eaf82-244">Aggiornare il database locale:</span><span class="sxs-lookup"><span data-stu-id="eaf82-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="eaf82-245">Digitare `Ctrl+F5` per eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="eaf82-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="eaf82-246">Testare i collegamenti Modifica, Dettagli e Crea.</span><span class="sxs-lookup"><span data-stu-id="eaf82-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="eaf82-247">Se l'applicazione viene caricata senza errori, l'esecuzione di Migrazioni Code First è stata completata.</span><span class="sxs-lookup"><span data-stu-id="eaf82-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="eaf82-248">La pagina tuttavia può apparire sempre uguale perché la logica dell'applicazione non usa ancora la nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="eaf82-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="eaf82-249">Usare la nuova proprietà</span><span class="sxs-lookup"><span data-stu-id="eaf82-249">Use the new property</span></span>

<span data-ttu-id="eaf82-250">Apportare alcune modifiche al codice per usare la proprietà `Done`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="eaf82-251">Per motivi di semplicità in questa esercitazione vengono modificate solo le visualizzazioni `Index` e `Create` per visualizzare la proprietà.</span><span class="sxs-lookup"><span data-stu-id="eaf82-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="eaf82-252">Aprire _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="eaf82-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="eaf82-253">Trovare il metodo `Create()` e aggiungere `Done` all'elenco delle proprietà nell'attributo `Bind`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="eaf82-254">Al termine, la firma del metodo `Create()` è simile al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf82-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="eaf82-255">Aprire _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="eaf82-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="eaf82-256">Nel codice Razor viene visualizzato un elemento `<div class="form-group">` che usa `model.Description` e quindi un altro elemento `<div class="form-group">` che usa `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="eaf82-257">Immediatamente dopo questi due elementi, aggiungere un altro elemento `<div class="form-group">` che usa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="eaf82-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="eaf82-258">Aprire _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="eaf82-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="eaf82-259">cercare l'elemento `<th></th>` vuoto.</span><span class="sxs-lookup"><span data-stu-id="eaf82-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="eaf82-260">Immediatamente sopra l'elemento, aggiungere il codice Razor seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf82-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="eaf82-261">Trovare l'elemento `<td>` che contiene i metodi helper `Html.ActionLink()`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="eaf82-262">Immediatamente sopra l'elemento, aggiungere il codice Razor seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf82-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="eaf82-263">Le modifiche verranno visualizzate nelle visualizzazioni `Index` e `Create`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="eaf82-264">Digitare `Ctrl+F5` per eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="eaf82-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="eaf82-265">È ora possibile aggiungere un'attività e selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="eaf82-266">L'attività viene visualizzata come completata nella home page.</span><span class="sxs-lookup"><span data-stu-id="eaf82-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="eaf82-267">Tenere presente che la visualizzazione `Edit` non mostra il campo `Done` poiché non è stata modificata la visualizzazione `Edit`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="eaf82-268">Abilitare Migrazioni Code First in Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="eaf82-269">Dopo aver completato la modifica al codice, inclusa la migrazione del database, la modifica viene pubblicata nell'app Web di Azure e viene eseguito l'aggiornamento del database SQL con Migrazioni Code First.</span><span class="sxs-lookup"><span data-stu-id="eaf82-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="eaf82-270">Fare di nuovo clic con il pulsante destro del mouse sul progetto e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="eaf82-271">Fare clic su **Impostazioni** per aprire la procedura guidata di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="eaf82-271">Click **Settings** to open the publish wizard.</span></span>

![Aprire le impostazioni di pubblicazione](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="eaf82-273">Nella procedura guidata fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="eaf82-274">Assicurarsi che la stringa di connessione per il database SQL sia popolata in **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="eaf82-275">Potrebbe essere necessario selezionare il database **myToDoAppDb** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="eaf82-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="eaf82-276">Selezionare **Esegui migrazione primo codice (inizia all'avvio dell'applicazione)**, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Abilitare Migrazioni Code First nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="eaf82-278">Pubblicare le modifiche</span><span class="sxs-lookup"><span data-stu-id="eaf82-278">Publish your changes</span></span>

<span data-ttu-id="eaf82-279">Dopo aver abilitato Migrazioni Code First nell'app Web di Azure pubblicare le modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="eaf82-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="eaf82-280">Nella pagina di pubblicazione fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="eaf82-281">Provare di nuovo ad aggiungere attività e selezionare **Fine**. Le attività verranno visualizzate nella home page come completate.</span><span class="sxs-lookup"><span data-stu-id="eaf82-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![App Web di Azure dopo la migrazione Code First](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="eaf82-283">Tutte le attività esistenti rimangono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="eaf82-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="eaf82-284">Quando si pubblica nuovamente l'applicazione ASP.NET, i dati esistenti nel database SQL non vengono persi.</span><span class="sxs-lookup"><span data-stu-id="eaf82-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="eaf82-285">Inoltre, solo Migrazioni Code First modifica lo schema dei dati lasciando intatti i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="eaf82-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="eaf82-286">Eseguire lo streaming dei log delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="eaf82-286">Stream application logs</span></span>

<span data-ttu-id="eaf82-287">È possibile eseguire lo streaming dei messaggi di traccia direttamente dall'app Web di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eaf82-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="eaf82-288">Aprire _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="eaf82-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="eaf82-289">Ogni azione inizia con un metodo `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="eaf82-290">Questo codice viene aggiunto per illustrare come aggiungere messaggi di traccia all'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="eaf82-291">Aprire Esplora server</span><span class="sxs-lookup"><span data-stu-id="eaf82-291">Open Server Explorer</span></span>

<span data-ttu-id="eaf82-292">Dal menu **Visualizza** selezionare **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="eaf82-293">È possibile configurare la registrazione per l'app Web di Azure in **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="eaf82-294">Abilitare lo streaming dei log</span><span class="sxs-lookup"><span data-stu-id="eaf82-294">Enable log streaming</span></span>

<span data-ttu-id="eaf82-295">In **Esplora server** espandere **Azure** > **Servizio app**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="eaf82-296">Espandere il gruppo di risorse **myResourceGroup** creato al momento della creazione dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="eaf82-297">Fare clic con il pulsante destro del mouse sull'app Web di Azure e scegliere **Visualizza log in streaming**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Abilitare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="eaf82-299">Lo streaming dei log viene eseguito nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-299">The logs are now streamed into the **Output** window.</span></span> 

![Streaming dei log nella finestra Output](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="eaf82-301">I messaggi di traccia tuttavia non sono ancora visibili.</span><span class="sxs-lookup"><span data-stu-id="eaf82-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="eaf82-302">Ciò avviene perché la prima volta che si seleziona **Visualizza log in streaming** l'app Web di Azure imposta il livello di traccia su `Error` che comporta soltanto la registrazione degli eventi di errore (con il metodo `Trace.TraceError()`).</span><span class="sxs-lookup"><span data-stu-id="eaf82-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="eaf82-303">Modificare i livelli di traccia</span><span class="sxs-lookup"><span data-stu-id="eaf82-303">Change trace levels</span></span>

<span data-ttu-id="eaf82-304">Per modificare i livelli di traccia per generare altri messaggi di traccia, tornare a **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="eaf82-305">Fare di nuovo clic con il pulsante destro del mouse sull'app Web di Azure e selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="eaf82-306">Nell'elenco a discesa **Registrazione applicazioni (file system)** selezionare **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="eaf82-307">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-307">Click **Save**.</span></span>

![Modificare il livello di traccia in Dettagli](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="eaf82-309">È possibile provare i diversi livelli di traccia per verificare i tipi di messaggi visualizzati per ogni livello.</span><span class="sxs-lookup"><span data-stu-id="eaf82-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="eaf82-310">Ad esempio, il livello **Informazioni** include tutti i log creati da `Trace.TraceInformation()`, `Trace.TraceWarning()` e `Trace.TraceError()`, ma non i log creati da `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="eaf82-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="eaf82-311">Nel browser provare a fare clic all'interno dell'applicazione dell'elenco attività in Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="eaf82-312">Viene eseguito lo streaming dei messaggi di traccia nella finestra **Output** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eaf82-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="eaf82-313">Arrestare lo streaming dei log</span><span class="sxs-lookup"><span data-stu-id="eaf82-313">Stop log streaming</span></span>

<span data-ttu-id="eaf82-314">Per arrestare il servizio di streaming dei log, fare clic sul pulsante **Interrompi monitoraggio** nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Arrestare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="eaf82-316">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-316">Manage your Azure web app</span></span>

<span data-ttu-id="eaf82-317">Accedere al [portale di Azure](https://portal.azure.com) per visualizzare l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="eaf82-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="eaf82-318">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf82-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="eaf82-320">Viene visualizzata la pagina dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="eaf82-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="eaf82-321">Per impostazione predefinita, il portale visualizza la pagina **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="eaf82-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="eaf82-322">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="eaf82-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="eaf82-323">In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="eaf82-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="eaf82-324">Le schede sul lato sinistro della pagina mostrano le diverse pagine di configurazione che è possibile aprire.</span><span class="sxs-lookup"><span data-stu-id="eaf82-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="eaf82-326">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eaf82-326">Next steps</span></span>

<span data-ttu-id="eaf82-327">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="eaf82-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaf82-328">Creare un database SQL in Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="eaf82-329">Connettere un'app ASP.NET al database SQL</span><span class="sxs-lookup"><span data-stu-id="eaf82-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="eaf82-330">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="eaf82-331">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="eaf82-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="eaf82-332">Eseguire lo streaming dei log da Azure al terminale</span><span class="sxs-lookup"><span data-stu-id="eaf82-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="eaf82-333">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="eaf82-334">Passare all'esercitazione successiva per apprendere come eseguire il mapping di un nome DNS personalizzato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="eaf82-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eaf82-335">Eseguire il mapping di un nome DNS personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf82-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
