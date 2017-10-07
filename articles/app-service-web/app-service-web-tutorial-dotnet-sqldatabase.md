---
title: un'applicazione ASP.NET in Azure con il Database SQL aaaBuild | Documenti Microsoft
description: Informazioni su come tooget un ASP.NET app Usa Azure, con tooa connessione Database SQL.
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="71bfd-103">Creare un'app ASP.NET in Azure con un database SQL</span><span class="sxs-lookup"><span data-stu-id="71bfd-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="71bfd-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="71bfd-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="71bfd-105">In questa esercitazione Mostra come toodeploy un ASP.NET basati sui dati web app in Azure e connetterla troppo[Database SQL di Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71bfd-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="71bfd-106">Al termine, si dispone di un'applicazione ASP.NET in esecuzione in [Azure App Service](../app-service/app-service-value-prop-what-is.md) e tooSQL Database connesso.</span><span class="sxs-lookup"><span data-stu-id="71bfd-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="71bfd-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="71bfd-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71bfd-109">Creare un database SQL in Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="71bfd-110">Connettersi a un tooSQL app ASP.NET Database</span><span class="sxs-lookup"><span data-stu-id="71bfd-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="71bfd-111">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="71bfd-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="71bfd-112">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="71bfd-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="71bfd-113">Registri di flusso di Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="71bfd-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="71bfd-114">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71bfd-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="71bfd-115">Prerequisites</span></span>

<span data-ttu-id="71bfd-116">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="71bfd-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="71bfd-117">Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello carichi di lavoro seguente:</span><span class="sxs-lookup"><span data-stu-id="71bfd-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="71bfd-118">**Sviluppo Web e ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="71bfd-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="71bfd-119">**Sviluppo di Azure**</span><span class="sxs-lookup"><span data-stu-id="71bfd-119">**Azure development**</span></span>

  ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="71bfd-121">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="71bfd-121">Download hello sample</span></span>

<span data-ttu-id="71bfd-122">[Scaricare il progetto di esempio hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="71bfd-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="71bfd-123">Estrarre (decomprimere) hello *master.zip dotnet-sqldb-esercitazione* file.</span><span class="sxs-lookup"><span data-stu-id="71bfd-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="71bfd-124">progetto di esempio Hello contiene un basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-lettura-aggiornamento-eliminazione) app usando [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="71bfd-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="71bfd-125">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="71bfd-125">Run hello app</span></span>

<span data-ttu-id="71bfd-126">Aprire hello *dotnet-sqldb-esercitazione-master/DotNetAppSqlDb.sln* file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71bfd-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="71bfd-127">Tipo `Ctrl+F5` toorun hello app senza debug.</span><span class="sxs-lookup"><span data-stu-id="71bfd-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="71bfd-128">Hello app viene visualizzata nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="71bfd-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="71bfd-129">Seleziona hello **Crea nuovo** collegare e creare un paio *attività* elementi.</span><span class="sxs-lookup"><span data-stu-id="71bfd-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Finestra di dialogo Nuovo progetto ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="71bfd-131">Hello test **modifica**, **dettagli**, e **eliminare** collegamenti.</span><span class="sxs-lookup"><span data-stu-id="71bfd-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="71bfd-132">app Hello Usa un tooconnect di contesto di database con database hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="71bfd-133">In questo esempio, il contesto di database hello utilizza una stringa di connessione denominata `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="71bfd-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="71bfd-134">stringa di connessione Hello è impostato in hello *Web. config* file e cui viene fatto riferimento in hello *Models/MyDatabaseContext.cs* file.</span><span class="sxs-lookup"><span data-stu-id="71bfd-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="71bfd-135">nome di stringa di connessione Hello viene utilizzato più avanti in hello tooconnect esercitazione hello Azure web app tooan Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="71bfd-136">Pubblicare tooAzure con il Database SQL</span><span class="sxs-lookup"><span data-stu-id="71bfd-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="71bfd-137">In hello **Esplora**, fare doppio clic sui **DotNetAppSqlDb** del progetto e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Pubblicare da Esplora soluzioni](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="71bfd-139">Verificare che **Servizio app di Microsoft Azure** sia selezionato e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="71bfd-141">Pubblicazione apre hello **Crea servizio App** finestra di dialogo, che consente di creare tutti hello risorse di Azure è necessario toorun app web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="71bfd-142">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="71bfd-142">Sign in tooAzure</span></span>

<span data-ttu-id="71bfd-143">In hello **Crea servizio App** finestra di dialogo, fare clic su **aggiungere un account**, quindi accedi tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="71bfd-144">Se si è già connessi a un account Microsoft, verificare che l'account contenga la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="71bfd-145">Se hello Microsoft account connesso non dispone di sottoscrizione di Azure, scegliere account di tooadd hello corretto.</span><span class="sxs-lookup"><span data-stu-id="71bfd-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Accedi tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="71bfd-147">Una volta effettuato l'accesso, si è pronti toocreate che tutte le risorse che necessarie per l'app web di Azure in questa finestra di dialogo di hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="71bfd-148">Nome dell'applicazione web hello configurare</span><span class="sxs-lookup"><span data-stu-id="71bfd-148">Configure hello web app name</span></span>

<span data-ttu-id="71bfd-149">È possibile mantenere nome dell'applicazione web hello generato o modificare il nome univoco tooanother (i caratteri validi sono `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="71bfd-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="71bfd-150">nome dell'applicazione web Hello viene utilizzata come parte dell'URL di hello predefinito per l'app (`<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'applicazione web).</span><span class="sxs-lookup"><span data-stu-id="71bfd-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="71bfd-151">nome dell'applicazione web Hello deve toobe univoco tra tutte le App in Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Finestra di dialogo Crea servizio app](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="71bfd-153">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="71bfd-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="71bfd-154">Avanti troppo**gruppo di risorse**, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-154">Next too**Resource Group**, click **New**.</span></span>

![TooResource successivo gruppo, fare clic su nuovo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="71bfd-156">Nome gruppo di risorse hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="71bfd-157">Non fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-157">Do not click **Create**.</span></span> <span data-ttu-id="71bfd-158">È necessario innanzitutto tooset di un Database SQL in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="71bfd-159">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="71bfd-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="71bfd-160">Avanti troppo**piano di servizio App**, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="71bfd-161">In hello **configurare il piano di servizio App** finestra di dialogo, configurare il nuovo piano di servizio App hello con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="71bfd-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Creare un piano di servizio app](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="71bfd-163">Impostazione</span><span class="sxs-lookup"><span data-stu-id="71bfd-163">Setting</span></span>  | <span data-ttu-id="71bfd-164">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="71bfd-164">Suggested value</span></span> | <span data-ttu-id="71bfd-165">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="71bfd-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="71bfd-166">**Piano di servizio app**</span><span class="sxs-lookup"><span data-stu-id="71bfd-166">**App Service Plan**</span></span>| <span data-ttu-id="71bfd-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="71bfd-167">myAppServicePlan</span></span> | [<span data-ttu-id="71bfd-168">Piani del servizio app</span><span class="sxs-lookup"><span data-stu-id="71bfd-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="71bfd-169">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="71bfd-169">**Location**</span></span>| <span data-ttu-id="71bfd-170">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="71bfd-170">West Europe</span></span> | [<span data-ttu-id="71bfd-171">Aree di Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="71bfd-172">**Dimensione**</span><span class="sxs-lookup"><span data-stu-id="71bfd-172">**Size**</span></span>| <span data-ttu-id="71bfd-173">Free</span><span class="sxs-lookup"><span data-stu-id="71bfd-173">Free</span></span> | [<span data-ttu-id="71bfd-174">Piani tariffari</span><span class="sxs-lookup"><span data-stu-id="71bfd-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="71bfd-175">Creare un'istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="71bfd-175">Create a SQL Server instance</span></span>

<span data-ttu-id="71bfd-176">Prima di creare un database è necessario un [server logico di database SQL di Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="71bfd-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="71bfd-177">Un server logico contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="71bfd-178">Selezionare **Esplora altri servizi di Azure**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-178">Select **Explore additional Azure services**.</span></span>

![Configurare il nome dell'app Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="71bfd-180">In hello **servizi** scheda, fare clic su hello  **+**  icona Avanti troppo**Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Nella scheda Servizi hello, fare clic sull'icona + hello tooSQL successivo Database.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="71bfd-182">In hello **configurare il Database SQL** finestra di dialogo, fare clic su **New** Avanti troppo**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="71bfd-183">Viene generato un nome di server univoco.</span><span class="sxs-lookup"><span data-stu-id="71bfd-183">A unique server name is generated.</span></span> <span data-ttu-id="71bfd-184">Questo nome viene utilizzato come parte dell'URL di hello predefinito per il server logico, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="71bfd-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="71bfd-185">Deve essere univoco in tutte le istanze di server logico in Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="71bfd-186">È possibile modificare il nome di server hello, ma per questa esercitazione, mantenere il valore di hello generato.</span><span class="sxs-lookup"><span data-stu-id="71bfd-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="71bfd-187">Aggiungere un nome utente e una password di amministratore e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="71bfd-188">Per i requisiti di complessità delle password, vedere [Criteri password](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="71bfd-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="71bfd-189">Prendere nota del nome utente e della password.</span><span class="sxs-lookup"><span data-stu-id="71bfd-189">Remember this username and password.</span></span> <span data-ttu-id="71bfd-190">Sono necessari server logico di hello toomanage istanza in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="71bfd-190">You need them toomanage hello logical server instance later.</span></span>

![Creare un'istanza di SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="71bfd-192">Creare un database SQL</span><span class="sxs-lookup"><span data-stu-id="71bfd-192">Create a SQL Database</span></span>

<span data-ttu-id="71bfd-193">In hello **configurare il Database SQL** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="71bfd-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="71bfd-194">Mantenere l'impostazione predefinita, hello generata **nome del Database**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="71bfd-195">In **Nome stringa di connessione** digitare *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="71bfd-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="71bfd-196">Questo nome deve corrispondere una stringa di connessione hello a cui fa riferimento in *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="71bfd-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="71bfd-197">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-197">Select **OK**.</span></span>

![Configurare il database SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="71bfd-199">Hello **Crea servizio App** finestra di dialogo Mostra risorse hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="71bfd-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="71bfd-200">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-200">Click **Create**.</span></span> 

![risorse Hello che è stato creato](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="71bfd-202">Al termine della procedura guidata hello creazione hello risorse di Azure, vengono pubblicati i tooAzure app ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="71bfd-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="71bfd-203">Il browser predefinito viene avviato con app di hello URL toohello distribuito.</span><span class="sxs-lookup"><span data-stu-id="71bfd-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="71bfd-204">Aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="71bfd-204">Add a few to-do items.</span></span>

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="71bfd-206">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="71bfd-206">Congratulations!</span></span> <span data-ttu-id="71bfd-207">L'applicazione ASP.NET basata sui dati è in esecuzione nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="71bfd-208">Accedere localmente hello Database SQL</span><span class="sxs-lookup"><span data-stu-id="71bfd-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="71bfd-209">Visual Studio consente di esplorare e gestire il nuovo Database SQL facilmente nel hello **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="71bfd-210">Creare una connessione al database</span><span class="sxs-lookup"><span data-stu-id="71bfd-210">Create a database connection</span></span>

<span data-ttu-id="71bfd-211">Da hello **vista** dal menu **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="71bfd-212">Nella parte superiore di hello di **Esplora oggetti di SQL Server**, fare clic su hello **aggiungere SQL Server** pulsante.</span><span class="sxs-lookup"><span data-stu-id="71bfd-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="71bfd-213">Configurare una connessione al database hello</span><span class="sxs-lookup"><span data-stu-id="71bfd-213">Configure hello database connection</span></span>

<span data-ttu-id="71bfd-214">In hello **Connetti** finestra di dialogo espandere hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="71bfd-215">Vengono visualizzate tutte le istanze del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="71bfd-216">Seleziona hello `DotNetAppSqlDb` Database SQL.</span><span class="sxs-lookup"><span data-stu-id="71bfd-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="71bfd-217">connessione Hello creata in precedenza viene inserito automaticamente nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="71bfd-218">Digitare hello password di amministratore di database creato in precedenza e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Configurare la connessione al database da Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="71bfd-220">Consentire la connessione client dal computer</span><span class="sxs-lookup"><span data-stu-id="71bfd-220">Allow client connection from your computer</span></span>

<span data-ttu-id="71bfd-221">Hello **creare una nuova regola firewall** è aperta una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="71bfd-222">Per impostazione predefinita, l'istanza del database SQL consente solo le connessioni da servizi di Azure, ad esempio dall'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="71bfd-223">tooconnect tooyour del database, creare una regola del firewall nell'istanza di Database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="71bfd-224">regola del firewall Hello consente hello indirizzo IP del computer locale.</span><span class="sxs-lookup"><span data-stu-id="71bfd-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="71bfd-225">finestra di dialogo Hello è già stato compilato con indirizzo IP pubblico del computer.</span><span class="sxs-lookup"><span data-stu-id="71bfd-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="71bfd-226">Assicurarsi che l'opzione **Aggiungi IP client** sia selezionata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Impostare il firewall per l'istanza del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="71bfd-228">Una volta terminato Visual Studio creazione hello impostazione del firewall per l'istanza del Database SQL, la connessione viene visualizzato nella **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="71bfd-229">In questo caso, è possibile eseguire hello più comuni operazioni di database, ad esempio le query eseguite, creano visualizzazioni e stored procedure e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="71bfd-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="71bfd-230">Fare clic su hello `Todoes` tabella e selezionare **Visualizza dati**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Esplorare gli oggetti del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="71bfd-232">Aggiornare l'app con Migrazioni Code First</span><span class="sxs-lookup"><span data-stu-id="71bfd-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="71bfd-233">È possibile utilizzare strumenti comuni di hello in Visual Studio tooupdate l'app web e il database in Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="71bfd-234">In questo passaggio utilizzare migrazioni Code First in Entity Framework toomake tooyour modifica uno schema di database e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="71bfd-235">Per altre informazioni sull'uso di Migrazioni Code First di Entity Framework, vedere [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Introduzione a Code First di Entity Framework 6 con MVC 5).</span><span class="sxs-lookup"><span data-stu-id="71bfd-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="71bfd-236">Aggiornare il modello di dati</span><span class="sxs-lookup"><span data-stu-id="71bfd-236">Update your data model</span></span>

<span data-ttu-id="71bfd-237">Aprire _Models\Todo.cs_ nell'editor di codice hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="71bfd-238">Aggiungere hello seguente proprietà toohello `ToDo` classe:</span><span class="sxs-lookup"><span data-stu-id="71bfd-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="71bfd-239">Eseguire Migrazioni Code First in locale</span><span class="sxs-lookup"><span data-stu-id="71bfd-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="71bfd-240">Eseguire alcuni comandi toomake aggiornamenti tooyour database locale.</span><span class="sxs-lookup"><span data-stu-id="71bfd-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="71bfd-241">Da hello **strumenti** menu, fare clic su **Gestione pacchetti NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="71bfd-242">Nella finestra della Console di gestione pacchetti hello, abilitare le migrazioni Code First:</span><span class="sxs-lookup"><span data-stu-id="71bfd-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="71bfd-243">Aggiungere una migrazione:</span><span class="sxs-lookup"><span data-stu-id="71bfd-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="71bfd-244">Aggiornamento del database locale hello:</span><span class="sxs-lookup"><span data-stu-id="71bfd-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="71bfd-245">Tipo `Ctrl+F5` toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="71bfd-246">Hello test, modificare, informazioni dettagliate, nonché creare collegamenti.</span><span class="sxs-lookup"><span data-stu-id="71bfd-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="71bfd-247">Se un'applicazione hello viene caricata senza errori, migrazioni Code First è stata completata.</span><span class="sxs-lookup"><span data-stu-id="71bfd-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="71bfd-248">Tuttavia, ha un aspetto ancora la pagina hello stesso poiché la logica dell'applicazione non utilizza ancora la nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="71bfd-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="71bfd-249">Utilizzare hello nuova proprietà</span><span class="sxs-lookup"><span data-stu-id="71bfd-249">Use hello new property</span></span>

<span data-ttu-id="71bfd-250">Apportare alcune modifiche nel hello toouse codice `Done` proprietà.</span><span class="sxs-lookup"><span data-stu-id="71bfd-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="71bfd-251">Per semplicità in questa esercitazione, sarà solo hello toochange `Index` e `Create` viste proprietà hello toosee nell'azione.</span><span class="sxs-lookup"><span data-stu-id="71bfd-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="71bfd-252">Aprire _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="71bfd-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="71bfd-253">Trovare hello `Create()` (metodo) e aggiungere `Done` toohello elenco delle proprietà hello `Bind` attributo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="71bfd-254">Al termine, il `Create()` firma del metodo è simile a hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="71bfd-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="71bfd-255">Aprire _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="71bfd-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="71bfd-256">Nel codice Razor hello, vedrai un `<div class="form-group">` elemento che utilizza `model.Description`e quindi un'altra `<div class="form-group">` elemento che utilizza `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="71bfd-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="71bfd-257">Immediatamente dopo questi due elementi, aggiungere un altro elemento `<div class="form-group">` che usa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="71bfd-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="71bfd-258">Aprire _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="71bfd-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="71bfd-259">Ricerca di hello vuoto `<th></th>` elemento.</span><span class="sxs-lookup"><span data-stu-id="71bfd-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="71bfd-260">Sopra questo elemento, aggiungere hello codice Razor seguenti:</span><span class="sxs-lookup"><span data-stu-id="71bfd-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="71bfd-261">Trovare hello `<td>` elemento contenente hello `Html.ActionLink()` metodi di supporto.</span><span class="sxs-lookup"><span data-stu-id="71bfd-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="71bfd-262">Sopra questo elemento, aggiungere hello codice Razor seguenti:</span><span class="sxs-lookup"><span data-stu-id="71bfd-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="71bfd-263">Che sono tutte le necessarie modifiche hello toosee hello `Index` e `Create` viste.</span><span class="sxs-lookup"><span data-stu-id="71bfd-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="71bfd-264">Tipo `Ctrl+F5` toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="71bfd-265">È ora possibile aggiungere un'attività e selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="71bfd-266">L'attività viene visualizzata come completata nella home page.</span><span class="sxs-lookup"><span data-stu-id="71bfd-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="71bfd-267">Tenere presente che hello `Edit` visualizzazione non mostra hello `Done` campo, perché non si sono modificati hello `Edit` visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="71bfd-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="71bfd-268">Abilitare Migrazioni Code First in Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="71bfd-269">Ora che il codice delle modifiche, inclusa la migrazione di database, si pubblicarla tooyour Azure web app e aggiorna il Database SQL con le migrazioni Code First troppo.</span><span class="sxs-lookup"><span data-stu-id="71bfd-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="71bfd-270">Fare di nuovo clic con il pulsante destro del mouse sul progetto e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="71bfd-271">Fare clic su **impostazioni** tooopen hello pubblicazione guidata.</span><span class="sxs-lookup"><span data-stu-id="71bfd-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Aprire le impostazioni di pubblicazione](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="71bfd-273">Nella procedura guidata hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="71bfd-274">Verificare che la stringa di connessione hello per il Database SQL viene popolato in **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="71bfd-275">Potrebbe essere necessario hello tooselect **myToDoAppDb** database dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="71bfd-276">Selezionare **Esegui migrazione primo codice (inizia all'avvio dell'applicazione)**, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Abilitare Migrazioni Code First nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="71bfd-278">Pubblicare le modifiche</span><span class="sxs-lookup"><span data-stu-id="71bfd-278">Publish your changes</span></span>

<span data-ttu-id="71bfd-279">Dopo aver abilitato Migrazioni Code First nell'app Web di Azure pubblicare le modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="71bfd-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="71bfd-280">In hello pagina pubblica, fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="71bfd-281">Provare di nuovo ad aggiungere attività e selezionare **Fine**. Le attività verranno visualizzate nella home page come completate.</span><span class="sxs-lookup"><span data-stu-id="71bfd-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![App Web di Azure dopo la migrazione Code First](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="71bfd-283">Tutte le attività esistenti rimangono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="71bfd-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="71bfd-284">Quando si pubblica nuovamente l'applicazione ASP.NET, i dati esistenti nel database SQL non vengono persi.</span><span class="sxs-lookup"><span data-stu-id="71bfd-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="71bfd-285">Inoltre, migrazioni Code First cambia solo schema dati hello e lascia intatti i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="71bfd-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="71bfd-286">Eseguire lo streaming dei log delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="71bfd-286">Stream application logs</span></span>

<span data-ttu-id="71bfd-287">È possibile trasmettere i messaggi di traccia direttamente il tooVisual app web di Azure Studio.</span><span class="sxs-lookup"><span data-stu-id="71bfd-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="71bfd-288">Aprire _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="71bfd-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="71bfd-289">Ogni azione inizia con un metodo `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="71bfd-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="71bfd-290">Questo codice viene aggiunto tooshow è la modalità tooadd traccia dei messaggi tooyour Azure web app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="71bfd-291">Aprire Esplora server</span><span class="sxs-lookup"><span data-stu-id="71bfd-291">Open Server Explorer</span></span>

<span data-ttu-id="71bfd-292">Da hello **vista** dal menu **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="71bfd-293">È possibile configurare la registrazione per l'app Web di Azure in **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="71bfd-294">Abilitare lo streaming dei log</span><span class="sxs-lookup"><span data-stu-id="71bfd-294">Enable log streaming</span></span>

<span data-ttu-id="71bfd-295">In **Esplora server** espandere **Azure** > **Servizio app**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="71bfd-296">Espandere hello **myResourceGroup** gruppo di risorse creato al momento della creazione hello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="71bfd-297">Fare clic con il pulsante destro del mouse sull'app Web di Azure e scegliere **Visualizza log in streaming**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Abilitare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="71bfd-299">Hello registri vengono ora trasmessi in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="71bfd-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Streaming dei log nella finestra Output](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="71bfd-301">Tuttavia, non viene visualizzato uno dei messaggi di traccia hello ancora.</span><span class="sxs-lookup"><span data-stu-id="71bfd-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="71bfd-302">Questo perché quando si seleziona prima **Visualizza log di Streaming**, l'app web di Azure consente di impostare il livello di traccia hello troppo`Error`, che registra solo gli eventi di errore (con hello `Trace.TraceError()` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="71bfd-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="71bfd-303">Modificare i livelli di traccia</span><span class="sxs-lookup"><span data-stu-id="71bfd-303">Change trace levels</span></span>

<span data-ttu-id="71bfd-304">traccia hello toochange livelli toooutput altri messaggi di traccia, passare nuovamente troppo**Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="71bfd-305">Fare di nuovo clic con il pulsante destro del mouse sull'app Web di Azure e selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="71bfd-306">In hello **registrazione delle applicazioni (File System)** elenco a discesa Seleziona **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="71bfd-307">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="71bfd-307">Click **Save**.</span></span>

![Modificare tooVerbose livello di traccia](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="71bfd-309">È possibile sperimentare toosee livelli diversi di traccia vengono visualizzati i tipi di messaggi per ogni livello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="71bfd-310">Ad esempio, hello **informazioni** livello include tutti i log creati da `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, ma non i log creati da `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="71bfd-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="71bfd-311">Nel browser, fare clic su intorno a un'applicazione elenco attività hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="71bfd-312">i messaggi di traccia Hello ora vengono trasmessi toohello **Output** finestra in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71bfd-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="71bfd-313">Arrestare lo streaming dei log</span><span class="sxs-lookup"><span data-stu-id="71bfd-313">Stop log streaming</span></span>

<span data-ttu-id="71bfd-314">toostop hello servizio flusso di log, fare clic su hello **interrompere il monitoraggio** pulsante hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="71bfd-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Arrestare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="71bfd-316">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-316">Manage your Azure web app</span></span>

<span data-ttu-id="71bfd-317">Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="71bfd-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="71bfd-318">Scegliere dal menu a sinistra hello **servizio App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="71bfd-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="71bfd-320">Viene visualizzata la pagina dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="71bfd-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="71bfd-321">Per impostazione predefinita, il portale di hello Mostra hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="71bfd-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="71bfd-322">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="71bfd-323">In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="71bfd-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="71bfd-324">schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello.</span><span class="sxs-lookup"><span data-stu-id="71bfd-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="71bfd-326">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71bfd-326">Next steps</span></span>

<span data-ttu-id="71bfd-327">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="71bfd-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71bfd-328">Creare un database SQL in Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="71bfd-329">Connettersi a un tooSQL app ASP.NET Database</span><span class="sxs-lookup"><span data-stu-id="71bfd-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="71bfd-330">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="71bfd-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="71bfd-331">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="71bfd-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="71bfd-332">Registri di flusso di Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="71bfd-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="71bfd-333">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="71bfd-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="71bfd-334">Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati toohello web app.</span><span class="sxs-lookup"><span data-stu-id="71bfd-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71bfd-335">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="71bfd-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
