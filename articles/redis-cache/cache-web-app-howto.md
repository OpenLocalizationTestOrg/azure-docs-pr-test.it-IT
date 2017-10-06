---
title: aaaHow toocreate un'App Web in Cache Redis | Documenti Microsoft
description: Informazioni su come toocreate un'App Web in Cache Redis
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="110eb-103">Come toocreate un'App Web in Cache Redis</span><span class="sxs-lookup"><span data-stu-id="110eb-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="110eb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="110eb-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="110eb-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="110eb-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="110eb-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="110eb-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="110eb-107">Java</span><span class="sxs-lookup"><span data-stu-id="110eb-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="110eb-108">Python</span><span class="sxs-lookup"><span data-stu-id="110eb-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="110eb-109">Questa esercitazione viene illustrato come toocreate e distribuire un'app web ASP.NET web applicazione tooa nel servizio App di Azure utilizzando Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="110eb-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="110eb-110">applicazione di esempio Hello Visualizza un elenco delle statistiche team da un database e illustra i diversi modi toouse Cache Redis di Azure toostore e recuperare i dati dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="110eb-111">Dopo aver completato l'esercitazione hello avrai un'app web in esecuzione che legge e scrive tooa database, ottimizzata con Cache Redis di Azure e ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="110eb-112">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="110eb-112">You'll learn:</span></span>

* <span data-ttu-id="110eb-113">Toocreate un MVC ASP.NET 5 web come applicazione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="110eb-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="110eb-114">Come tooaccess dati da un database tramite Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="110eb-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="110eb-115">La velocità effettiva dei dati tooimprove e ridurre il carico di database per l'archiviazione e recupero di dati tramite una Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="110eb-116">La modalità di ordinamento set tooretrieve hello top 5 team toouse un Redis.</span><span class="sxs-lookup"><span data-stu-id="110eb-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="110eb-117">Tooprovision hello come risorse di Azure per un'applicazione hello utilizzando un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="110eb-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="110eb-118">Come toopublish hello tooAzure applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="110eb-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="110eb-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="110eb-119">Prerequisites</span></span>
<span data-ttu-id="110eb-120">esercitazione di hello toocomplete, è necessario disporre di hello seguenti prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="110eb-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="110eb-121">Account di Azure</span><span class="sxs-lookup"><span data-stu-id="110eb-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="110eb-122">Visual Studio 2017 con hello Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="110eb-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="110eb-123">Account Azure</span><span class="sxs-lookup"><span data-stu-id="110eb-123">Azure account</span></span>
<span data-ttu-id="110eb-124">È necessario un'esercitazione di hello toocomplete account Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="110eb-125">È possibile:</span><span class="sxs-lookup"><span data-stu-id="110eb-125">You can:</span></span>

* <span data-ttu-id="110eb-126">[Aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero):</span><span class="sxs-lookup"><span data-stu-id="110eb-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="110eb-127">È possibile ottenere crediti che possono essere utilizzati tootry out a pagamento di servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="110eb-128">Anche dopo hello crediti, è possibile tenere conto di hello e utilizzare le funzionalità e servizi di Azure gratuiti.</span><span class="sxs-lookup"><span data-stu-id="110eb-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="110eb-129">[Attivare i vantaggi della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="110eb-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="110eb-130">con l'abbonamento MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="110eb-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="110eb-131">Visual Studio 2017 con hello Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="110eb-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="110eb-132">è stato scritto per Visual Studio 2017 esercitazione Hello con hello [Azure SDK per .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="110eb-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="110eb-133">Azure SDK 2.9.5 Hello è incluso con il programma di installazione di hello Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="110eb-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="110eb-134">Se si dispone di Visual Studio 2015, è possibile seguire l'esercitazione hello con hello [Azure SDK per .NET](../dotnet-sdk.md) 2.8.2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="110eb-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="110eb-135">[Download hello SDK più recente di Azure per Visual Studio 2015 qui](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="110eb-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="110eb-136">Visual Studio viene installato automaticamente con hello SDK se non si dispone già.</span><span class="sxs-lookup"><span data-stu-id="110eb-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="110eb-137">Alcuni schermi potrebbero essere diverse dalle immagini raffigurate hello illustrate in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="110eb-138">Se si dispone di Visual Studio 2013, è possibile [download hello SDK più recente di Azure per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="110eb-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="110eb-139">Alcuni schermi potrebbero essere diverse dalle immagini raffigurate hello illustrate in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="110eb-140">Creare il progetto di Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="110eb-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="110eb-141">Aprire Visual Studio e fare clic su **File**, **Nuovo**, **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="110eb-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="110eb-142">Espandere hello **Visual c#** nodo hello **modelli** elenco, selezionare **Cloud**, fare clic su **applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="110eb-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="110eb-143">Assicurarsi che sia selezionata l'opzione **.NET Framework 4.5.2** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="110eb-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="110eb-144">Tipo **ContosoTeamStats** in hello **nome** casella di testo e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="110eb-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Crea progetto][cache-create-project]
3. <span data-ttu-id="110eb-146">Selezionare **MVC** come tipo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="110eb-147">Verificare che **Nessuna autenticazione** specificato per hello **autenticazione** impostazioni.</span><span class="sxs-lookup"><span data-stu-id="110eb-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="110eb-148">A seconda della versione di Visual Studio, predefinito hello è possibile impostare toosomething else.</span><span class="sxs-lookup"><span data-stu-id="110eb-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="110eb-149">toochange, fare clic su **Modifica autenticazione** e selezionare **Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="110eb-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="110eb-150">Se si segue insieme a Visual Studio 2015, deselezionare hello **Host nel cloud hello** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="110eb-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="110eb-151">Sarà necessario [provisioning hello risorse di Azure](#provision-the-azure-resources) e [pubblicare tooAzure applicazione hello](#publish-the-application-to-azure) nei passaggi successivi dell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="110eb-152">Per un esempio di provisioning di un'applicazione di servizio App web da Visual Studio lasciando **Host nel cloud hello** selezionata, vedere [iniziare con le app Web in Azure App Service, con ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="110eb-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Seleziona modello progetto][cache-select-template]
4. <span data-ttu-id="110eb-154">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="110eb-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="110eb-155">Creare hello applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="110eb-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="110eb-156">In questa sezione dell'esercitazione hello, si creerà un'applicazione hello base che legge e visualizza le statistiche team da un database.</span><span class="sxs-lookup"><span data-stu-id="110eb-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="110eb-157">Aggiungere il pacchetto NuGet di Entity Framework hello</span><span class="sxs-lookup"><span data-stu-id="110eb-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="110eb-158">Aggiungere modello hello</span><span class="sxs-lookup"><span data-stu-id="110eb-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="110eb-159">Aggiungi controller hello</span><span class="sxs-lookup"><span data-stu-id="110eb-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="110eb-160">Configurare le visualizzazioni di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="110eb-161">Aggiungere il pacchetto NuGet di Entity Framework hello</span><span class="sxs-lookup"><span data-stu-id="110eb-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="110eb-162">Fare clic su **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.</span><span class="sxs-lookup"><span data-stu-id="110eb-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="110eb-163">Esecuzione hello il seguente comando da hello **Package Manager Console** finestra.</span><span class="sxs-lookup"><span data-stu-id="110eb-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="110eb-164">Per ulteriori informazioni sul pacchetto, vedere hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) pagina NuGet.</span><span class="sxs-lookup"><span data-stu-id="110eb-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="110eb-165">Aggiungere modello hello</span><span class="sxs-lookup"><span data-stu-id="110eb-165">Add hello model</span></span>
1. <span data-ttu-id="110eb-166">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="110eb-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Aggiungi modello][cache-model-add-class]
2. <span data-ttu-id="110eb-168">Immettere `Team` nome della classe hello e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="110eb-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Aggiunta di una classe modello][cache-model-add-class-dialog]
3. <span data-ttu-id="110eb-170">Sostituire hello `using` le istruzioni nella parte superiore di hello di hello `Team.cs` file con il seguente hello `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="110eb-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="110eb-171">Sostituire la definizione hello di hello `Team` classe con hello seguente frammento di codice che contiene una versione aggiornata `Team` classe definizione, nonché alcune altre classi di supporto di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="110eb-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="110eb-172">Per ulteriori informazioni su hello codice primo approccio tooEntity Framework che viene utilizzato in questa esercitazione, vedere [codice prima tooa nuovo database](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="110eb-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="110eb-173">In **Esplora**, fare doppio clic su **Web. config** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="110eb-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="110eb-175">Aggiungere il seguente hello `connectionStrings` sezione.</span><span class="sxs-lookup"><span data-stu-id="110eb-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="110eb-176">nome di Hello hello della stringa di connessione deve corrispondere hello nome di classe del contesto del database di Entity Framework che è hello `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="110eb-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="110eb-177">È possibile aggiungere nuovi hello `connectionStrings` sezione in modo che segua `configSections`, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="110eb-178">La stringa di connessione potrebbe essere diversa a seconda della versione di hello di Visual Studio e SQL Server Express edition utilizzato esercitazione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="110eb-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="110eb-179">modello di Hello Web. config deve essere configurato toomatch l'installazione e può contenere `Data Source` come voci `(LocalDB)\v11.0` (da SQL Server Express 2012) o `Data Source=(LocalDB)\MSSQLLocalDB` (da SQL Server Express 2014 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="110eb-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="110eb-180">Per altre informazioni sulle stringhe di connessione e le versioni di SQL Express, vedere [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="110eb-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="110eb-181">Aggiungi controller hello</span><span class="sxs-lookup"><span data-stu-id="110eb-181">Add hello controller</span></span>
1. <span data-ttu-id="110eb-182">Premere **F6** progetto hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="110eb-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="110eb-183">In **Esplora**, hello rapida **controller** cartella e scegliere **Aggiungi**, **Controller**.</span><span class="sxs-lookup"><span data-stu-id="110eb-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Aggiungi controller][cache-add-controller]
3. <span data-ttu-id="110eb-185">Scegliere **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="110eb-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="110eb-186">Se si verifica un errore dopo aver fatto clic **Aggiungi**, assicurarsi che siano compilati prima di tutto il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Aggiunta di una classe controller][cache-add-controller-class]
4. <span data-ttu-id="110eb-188">Selezionare **Team (ContosoTeamStats.Models)** da hello **classe modello** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="110eb-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="110eb-189">Selezionare **TeamContext (ContosoTeamStats.Models)** da hello **classe contesto dati** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="110eb-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="110eb-190">Tipo `TeamsController` in hello **Controller** casella di testo Nome (se non è stato automaticamente popolata).</span><span class="sxs-lookup"><span data-stu-id="110eb-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="110eb-191">Fare clic su **Aggiungi** toocreate hello classe controller e aggiungere visualizzazioni predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Configura controller][cache-configure-controller]
5. <span data-ttu-id="110eb-193">In **Esplora**, espandere **Global. asax** fare doppio clic su **Global.asax.cs** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="110eb-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="110eb-195">Aggiungere i seguenti due hello `using` istruzioni all'inizio di hello del file hello in altri hello `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="110eb-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="110eb-196">Aggiungere hello successiva riga di codice alla fine hello hello `Application_Start` metodo.</span><span class="sxs-lookup"><span data-stu-id="110eb-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="110eb-197">In **Esplora soluzioni** espandere `App_Start` e fare doppio clic su `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="110eb-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="110eb-199">Sostituire `controller = "Home"` nel seguente codice hello hello `RegisterRoutes` metodo con `controller = "Teams"` come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="110eb-200">Configurare le visualizzazioni di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-200">Configure hello views</span></span>
1. <span data-ttu-id="110eb-201">In **Esplora**, espandere hello **viste** cartella e quindi hello **Shared** cartella e fare doppio clic **layout. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="110eb-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![file _Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="110eb-203">Modificare il contenuto di hello di hello `title` elemento e sostituire `My ASP.NET Application` con `Contoso Team Stats` come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="110eb-204">In hello `body` sezione, aggiornare innanzitutto hello `Html.ActionLink` istruzione e sostituire `Application name` con `Contoso Team Stats` e sostituire `Home` con `Teams`.</span><span class="sxs-lookup"><span data-stu-id="110eb-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="110eb-205">Prima: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="110eb-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="110eb-206">Dopo: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="110eb-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Modifiche al codice][cache-layout-cshtml-code]
2. <span data-ttu-id="110eb-208">Premere **Ctrl + F5** toobuild ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="110eb-209">Questa versione di un'applicazione hello legge risultati hello direttamente dal database di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="110eb-210">Hello nota **Crea nuovo**, **modifica**, **dettagli**, e **eliminare** azioni che sono stati automaticamente aggiunti applicazione toohello da hello **Controller MVC 5 con visualizzazioni, mediante Entity Framework** lo scaffolding.</span><span class="sxs-lookup"><span data-stu-id="110eb-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="110eb-211">Nella sezione successiva di hello di esercitazione hello aggiungerai accesso ai dati di Cache Redis toooptimize hello e forniscono funzionalità aggiuntive toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Applicazione iniziale][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="110eb-213">Configurare toouse applicazione hello Cache Redis</span><span class="sxs-lookup"><span data-stu-id="110eb-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="110eb-214">In questa sezione dell'esercitazione hello sarà configurare toostore applicazione di esempio hello e recuperare statistiche squadra Contoso da un'istanza di Cache Redis di Azure tramite hello [stackexchange. Redis](https://github.com/StackExchange/StackExchange.Redis) client della cache.</span><span class="sxs-lookup"><span data-stu-id="110eb-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="110eb-215">Configurare toouse applicazione hello stackexchange. Redis</span><span class="sxs-lookup"><span data-stu-id="110eb-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="110eb-216">Aggiornare i risultati di hello TeamsController classe tooreturn dalla cache di hello o database hello</span><span class="sxs-lookup"><span data-stu-id="110eb-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="110eb-217">Hello crea, modifica, aggiornare ed eliminare toowork metodi con cache di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="110eb-218">Aggiornare hello team indice vista toowork con cache di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="110eb-219">Configurare toouse applicazione hello stackexchange. Redis</span><span class="sxs-lookup"><span data-stu-id="110eb-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="110eb-220">Fare clic su un'applicazione client in Visual Studio usando il pacchetto NuGet stackexchange. Redis, hello tooconfigure **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.</span><span class="sxs-lookup"><span data-stu-id="110eb-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="110eb-221">Esecuzione hello il seguente comando da hello `Package Manager Console` finestra.</span><span class="sxs-lookup"><span data-stu-id="110eb-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="110eb-222">Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly per il tooaccess di applicazione client Cache Redis di Azure con i client della cache di hello stackexchange. Redis.</span><span class="sxs-lookup"><span data-stu-id="110eb-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="110eb-223">Se si preferisce una versione con nome sicuro di hello toouse `StackExchange.Redis` libreria client, installare hello `StackExchange.Redis.StrongName` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="110eb-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="110eb-224">In **Esplora**, espandere hello **controller** cartella e fare doppio clic su **TeamsController.cs** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="110eb-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Controller Teams][cache-teamscontroller]
4. <span data-ttu-id="110eb-226">Aggiungere i seguenti due hello `using` istruzioni troppo**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="110eb-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="110eb-227">Aggiungere i seguenti due proprietà toohello hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="110eb-227">Add hello following two properties toohello `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="110eb-228">Creare un file nel computer denominato `WebAppPlusCacheAppSecrets.config` e inserirle in un percorso che non è selezionata con il codice sorgente hello dell'applicazione di esempio, se si decide di toocheck in una posizione.</span><span class="sxs-lookup"><span data-stu-id="110eb-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="110eb-229">In questo hello esempio `AppSettingsSecrets.config` file si trova in `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="110eb-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="110eb-230">Modifica hello `WebAppPlusCacheAppSecrets.config` aggiungere hello seguente contenuto e dei file.</span><span class="sxs-lookup"><span data-stu-id="110eb-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="110eb-231">Se si esegue un'applicazione hello localmente queste informazioni sono l'istanza di Cache Redis di Azure di tooyour tooconnect utilizzato.</span><span class="sxs-lookup"><span data-stu-id="110eb-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="110eb-232">Più avanti nell'esercitazione di hello consentiranno di eseguire il provisioning di un'istanza di Cache Redis di Azure di aggiornare password e nome della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="110eb-233">Se non si prevede di applicazione di esempio hello toorun locale è possibile ignorare la creazione di hello di questo file e i passaggi successivi hello che fanno riferimento a file hello, perché quando si distribuisce un'applicazione hello tooAzure recupera le informazioni di connessione della cache di hello da app hello l'impostazione per hello App Web e non da questo file.</span><span class="sxs-lookup"><span data-stu-id="110eb-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="110eb-234">Poiché hello `WebAppPlusCacheAppSecrets.config` non è stato distribuito tooAzure con l'applicazione, non è necessario a meno che non si intende un'applicazione hello toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="110eb-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="110eb-235">In **Esplora**, fare doppio clic su **Web. config** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="110eb-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="110eb-237">Aggiungere il seguente hello `file` attributo toohello `appSettings` elemento.</span><span class="sxs-lookup"><span data-stu-id="110eb-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="110eb-238">Se si utilizza un altro nome di file o un percorso, sostituire i valori per hello quelli illustrati nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="110eb-239">Prima: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="110eb-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="110eb-240">Dopo: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="110eb-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="110eb-241">il runtime ASP.NET Hello unisce il contenuto di hello del file esterno di hello con markup hello in hello `<appSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="110eb-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="110eb-242">Se non è possibile trovare il file specificato hello, Hello runtime ignora dell'attributo del file hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="110eb-243">I segreti (cache di tooyour stringhe di connessione di hello) non sono inclusi come parte del codice sorgente hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="110eb-244">Quando si distribuisce il tooAzure app web, hello `WebAppPlusCacheAppSecrests.config` file non verrà distribuito (che è quello desiderato).</span><span class="sxs-lookup"><span data-stu-id="110eb-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="110eb-245">Sono disponibili diversi modi toospecify questi segreti in Azure e in questa esercitazione vengono configurate automaticamente per l'utente quando si [provisioning hello risorse di Azure](#provision-the-azure-resources) in un passaggio successivo dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="110eb-246">Per ulteriori informazioni sull'utilizzo dei segreti in Azure, vedere [procedure consigliate per la distribuzione delle password e altri dati sensibili tooASP.NET e servizio App di Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="110eb-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="110eb-247">Aggiornare i risultati di hello TeamsController classe tooreturn dalla cache di hello o database hello</span><span class="sxs-lookup"><span data-stu-id="110eb-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="110eb-248">In questo esempio, le statistiche del team possono essere recuperate dal database hello o dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="110eb-249">Statistiche squadra vengono memorizzate nella cache di hello come serializzata `List<Team>`e anche come un set ordinato utilizzando tipi di dati Redis.</span><span class="sxs-lookup"><span data-stu-id="110eb-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="110eb-250">Quando si recuperano elementi da un set ordinato, è possibile recuperare alcuni o tutti gli elementi o eseguire query per determinati elementi.</span><span class="sxs-lookup"><span data-stu-id="110eb-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="110eb-251">In questo esempio query verranno eseguite su set hello ordinato per hello top 5 i team classificati in base al numero di wins.</span><span class="sxs-lookup"><span data-stu-id="110eb-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="110eb-252">Non è necessario toostore hello team statistiche in più formati nella cache di hello in ordine toouse Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="110eb-253">Questa esercitazione viene utilizzato più formati toodemonstrate alcuni modi diversi di hello e tipi di dati diversi è possibile utilizzare dati toocache.</span><span class="sxs-lookup"><span data-stu-id="110eb-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="110eb-254">Aggiungere il seguente hello `using` istruzioni toohello `TeamsController.cs` file nella parte superiore di hello con altri hello `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="110eb-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="110eb-255">Sostituire hello corrente `public ActionResult Index()` implementazione del metodo con hello seguito all'implementazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="110eb-256">Aggiungere i seguenti tre metodi toohello hello `TeamsController` hello tooimplement classe `playGames`, `clearCache`, e `rebuildDB` tipi di azione da hello passare istruzione aggiunta nel frammento di codice precedente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="110eb-257">Hello `PlayGames` metodo Aggiorna statistiche squadra hello simulando una stagione dei giochi, Salva hello toohello database dei risultati e Cancella hello aggiornate dei dati dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="110eb-258">Hello `RebuildDB` metodo reinizializza hello database con il set predefinito di hello del team, genera le statistiche per essi, e Cancella hello aggiornate dei dati dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="110eb-259">Hello `ClearCachedTeams` metodo rimuove tutte le statistiche team memorizzati nella cache dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="110eb-260">Aggiungere i seguenti quattro metodi toohello hello `TeamsController` hello tooimplement classe varie modalità di recupero di statistiche squadra hello dalla cache di hello e database hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="110eb-261">Ognuno di questi metodi restituisce un `List<Team>` che viene quindi visualizzato dalla visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="110eb-262">Hello `GetFromDB` metodo legge statistiche squadra hello dal database hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="110eb-263">Hello `GetFromList` metodo legge statistiche squadra hello dalla cache come serializzata `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="110eb-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="110eb-264">Se è presente un mancato riscontro nella cache, statistiche squadra hello sono lette dal database di hello e quindi memorizzate nella cache di hello per la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="110eb-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="110eb-265">In questo esempio si utilizza JSON.NET serializzazione tooserialize hello .NET oggetti tooand dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="110eb-266">Per ulteriori informazioni, vedere [come toowork con .NET gli oggetti nella Cache Redis di Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="110eb-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="110eb-267">Hello `GetFromSortedSet` metodo legge statistiche squadra hello da un set ordinato memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="110eb-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="110eb-268">Se è presente un mancato riscontro nella cache, statistiche squadra hello sono lette dal database di hello e memorizzate nella cache di hello come un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="110eb-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="110eb-269">Hello `GetFromSortedSetTop5` metodo legge insieme 5 team dal memorizzati nella cache di hello ordinati superiore hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="110eb-270">Avvia il controllo della cache di hello esistenza hello di hello `teamsSortedSet` chiave.</span><span class="sxs-lookup"><span data-stu-id="110eb-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="110eb-271">Se questa chiave non è presente, hello `GetFromSortedSet` metodo viene chiamato statistiche squadra di tooread hello e memorizzarli nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="110eb-272">Successivamente, hello set ordinato memorizzati nella cache viene eseguita una query per hello top 5 i team che vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="110eb-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="110eb-273">Hello crea, modifica, aggiornare ed eliminare toowork metodi con cache di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="110eb-274">codice di scaffolding Hello generato come parte di questo esempio include metodi tooadd, modificare ed eliminare i team.</span><span class="sxs-lookup"><span data-stu-id="110eb-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="110eb-275">Ogni volta che un team viene aggiunto, modificato o rimosso, i dati di hello nella cache di hello diventano obsoleti.</span><span class="sxs-lookup"><span data-stu-id="110eb-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="110eb-276">In questa sezione che si desidera modificare queste hello tooclear tre metodi memorizzati nella cache i team in modo che la cache di hello non verrà sincronizzata con il database di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="110eb-277">Sfoglia toohello `Create(Team team)` metodo hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="110eb-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="110eb-278">Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="110eb-279">Sfoglia toohello `Edit(Team team)` metodo hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="110eb-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="110eb-280">Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="110eb-281">Sfoglia toohello `DeleteConfirmed(int id)` metodo hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="110eb-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="110eb-282">Aggiungere una chiamata toohello `ClearCachedTeams` (metodo), come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="110eb-283">Aggiornare hello team indice vista toowork con cache di hello</span><span class="sxs-lookup"><span data-stu-id="110eb-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="110eb-284">In **Esplora**, espandere hello **viste** cartella, quindi hello **Team** cartella e fare doppio clic **cshtml**.</span><span class="sxs-lookup"><span data-stu-id="110eb-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="110eb-286">Parte superiore di hello del file hello, cercare hello dopo l'elemento del paragrafo.</span><span class="sxs-lookup"><span data-stu-id="110eb-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Tabella delle azioni][cache-teams-index-table]
   
    <span data-ttu-id="110eb-288">Si tratta di hello collegamento toocreate un nuovo team.</span><span class="sxs-lookup"><span data-stu-id="110eb-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="110eb-289">Sostituire l'elemento del paragrafo hello con hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="110eb-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="110eb-290">La tabella include collegamenti ad azioni per la creazione di un nuovo team, la riproduzione di una nuovo stagione dei giochi, la cancellazione della cache di hello, recupero team hello dalla cache di hello in diversi formati, il recupero dei team hello dal database hello e ricompilare hello database con dati di esempio aggiornato.</span><span class="sxs-lookup"><span data-stu-id="110eb-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="110eb-291">Scorri toohello alla fine di hello **cshtml** file e aggiungere il seguente hello `tr` elemento in modo che venga hello ultima riga hello ultima tabella nel file hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="110eb-292">Questa riga viene visualizzato il valore di hello di `ViewBag.Msg` che contiene un report di stato sull'operazione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="110eb-293">Hello `ViewBag.Msg` viene impostato quando si fa clic su uno dei collegamenti di azione hello dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Messaggio di stato][cache-status-message]
2. <span data-ttu-id="110eb-295">Premere **F6** progetto hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="110eb-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="110eb-296">Eseguire il provisioning hello risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="110eb-296">Provision hello Azure resources</span></span>
<span data-ttu-id="110eb-297">toohost dell'applicazione in Azure, è necessario innanzitutto eseguire il provisioning di servizi di Azure che richiede l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="110eb-298">applicazione di esempio Hello in questa esercitazione Usa hello seguenti servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="110eb-299">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="110eb-299">Azure Redis Cache</span></span>
* <span data-ttu-id="110eb-300">App Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="110eb-300">App Service Web App</span></span>
* <span data-ttu-id="110eb-301">Database SQL</span><span class="sxs-lookup"><span data-stu-id="110eb-301">SQL Database</span></span>

<span data-ttu-id="110eb-302">toodeploy gruppo di risorse nuove o esistenti tooa questi servizi di propria scelta, fare clic su hello seguente **distribuire tooAzure** pulsante.</span><span class="sxs-lookup"><span data-stu-id="110eb-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="110eb-303">[! [Deploy tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="110eb-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="110eb-304">Questo **distribuire tooAzure** pulsante utilizza hello [creare un'App Web più Cache Redis di più Database SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) modello tooprovision tali servizi e hello set stringa di connessione per l'impostazione di applicazione di Database SQL e hello hello per hello stringa di connessione della Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="110eb-305">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="110eb-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="110eb-306">Facendo clic su hello **distribuire tooAzure** pulsante accetta toohello portale di Azure e avvia hello processo di creazione di risorse hello descritte da modello hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Distribuire tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="110eb-308">In hello **nozioni di base** sezione hello toouse di sottoscrizione di Azure, selezionare e selezionare un gruppo di risorse esistente o crearne uno nuovo e specificare il percorso del gruppo risorse hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="110eb-309">In hello **impostazioni** sezione, specificare un **account di accesso amministratore** (non utilizzare **admin**), **Password dell'account di accesso amministratore**e  **Nome del database**.</span><span class="sxs-lookup"><span data-stu-id="110eb-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="110eb-310">Hello altri parametri configurati per un servizio App gratuito piano e le opzioni di basso costo per Database SQL di hello e Cache Redis di Azure, che non provengono con un livello gratuito di hosting.</span><span class="sxs-lookup"><span data-stu-id="110eb-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Distribuire tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="110eb-312">Dopo aver configurato le impostazioni di hello desiderato, scorrere toohello fine pagina hello, hello leggere le condizioni e controllare hello **accetto le condizioni indicate in precedenza toohello** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="110eb-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="110eb-313">Fare clic su toobegin durante il provisioning delle risorse hello, **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="110eb-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="110eb-314">stato di avanzamento hello tooview della distribuzione, fare clic sull'icona di notifica hello e fare clic su **distribuzione avviata**.</span><span class="sxs-lookup"><span data-stu-id="110eb-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![La distribuzione è stata avviata][cache-deployment-started]

<span data-ttu-id="110eb-316">È possibile visualizzare lo stato di hello della distribuzione su hello **Microsoft.Template** blade.</span><span class="sxs-lookup"><span data-stu-id="110eb-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Distribuire tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="110eb-318">Al termine il provisioning, è possibile pubblicare tooAzure l'applicazione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="110eb-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="110eb-319">Sono visualizzati eventuali errori che possono verificarsi durante il processo di provisioning hello in hello **Microsoft.Template** blade.</span><span class="sxs-lookup"><span data-stu-id="110eb-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="110eb-320">Gli errori comuni sono relativi a un numero eccessivo di server SQL o di piani di hosting del Servizio app gratuito per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="110eb-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="110eb-321">Risolvere gli eventuali errori e riavviare il processo di hello facendo **ridistribuire** su hello **Microsoft.Template** pannello o hello **distribuire tooAzure** pulsante in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="110eb-322">Pubblicare tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="110eb-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="110eb-323">In questo passaggio dell'esercitazione hello, si sarà pubblicare tooAzure applicazione hello ed eseguirlo nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="110eb-324">Pulsante destro del mouse hello **ContosoTeamStats** sul progetto in Visual Studio e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="110eb-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Pubblica][cache-publish-app]
2. <span data-ttu-id="110eb-326">Fare clic su **Servizio app di Microsoft Azure**, scegliere **Seleziona esistente** e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="110eb-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Pubblica][cache-publish-to-app-service]
3. <span data-ttu-id="110eb-328">Selezionare la sottoscrizione di hello utilizzata quando la creazione di risorse di Azure, hello espandere il gruppo di risorse hello contenente risorse hello e seleziona hello desiderato App Web.</span><span class="sxs-lookup"><span data-stu-id="110eb-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="110eb-329">Se è stato utilizzato hello **distribuire tooAzure** pulsante il nome dell'App Web inizia con **sito Web** seguita da alcuni caratteri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="110eb-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Selezione dell'app Web][cache-select-web-app]
4. <span data-ttu-id="110eb-331">Fare clic su **OK** hello toobegin processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="110eb-332">Dopo alcuni istanti completa hello processo di pubblicazione e un browser viene avviato con hello in esecuzione l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="110eb-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="110eb-333">Se è visualizzato un errore DNS durante la convalida o la pubblicazione e hello processo per il provisioning hello risorse Azure per un'applicazione hello ha appena completata di recente, attendere qualche istante e riprovare.</span><span class="sxs-lookup"><span data-stu-id="110eb-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache aggiunta][cache-added-to-application]

<span data-ttu-id="110eb-335">Hello nella tabella seguente descrive ciascun collegamento all'azione dall'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="110eb-336">Azione</span><span class="sxs-lookup"><span data-stu-id="110eb-336">Action</span></span> | <span data-ttu-id="110eb-337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="110eb-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="110eb-338">Creazione di un nuovo sito</span><span class="sxs-lookup"><span data-stu-id="110eb-338">Create New</span></span> |<span data-ttu-id="110eb-339">Crea un nuovo team.</span><span class="sxs-lookup"><span data-stu-id="110eb-339">Create a new Team.</span></span> |
| <span data-ttu-id="110eb-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="110eb-340">Play Season</span></span> |<span data-ttu-id="110eb-341">Riprodurre una stagione dei giochi, statistiche team hello di aggiornamento, e cancella qualsiasi obsoleta dati dalla cache di hello del team.</span><span class="sxs-lookup"><span data-stu-id="110eb-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="110eb-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="110eb-342">Clear Cache</span></span> |<span data-ttu-id="110eb-343">Statistiche del team crittografato hello dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="110eb-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="110eb-344">List from Cache</span></span> |<span data-ttu-id="110eb-345">Recuperare statistiche team hello dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="110eb-346">Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database di hello e salvare toohello cache per la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="110eb-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="110eb-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="110eb-347">Sorted Set from Cache</span></span> |<span data-ttu-id="110eb-348">Recuperare statistiche team hello dalla cache di hello con un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="110eb-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="110eb-349">Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database hello e salvare la cache toohello tramite un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="110eb-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="110eb-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="110eb-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="110eb-351">Recuperare i team di 5 superiore hello dalla cache di hello con un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="110eb-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="110eb-352">Se è presente un mancato riscontro nella cache, caricare statistiche hello dal database hello e salvare la cache toohello tramite un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="110eb-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="110eb-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="110eb-353">Load from DB</span></span> |<span data-ttu-id="110eb-354">Recuperare statistiche team hello dal database di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="110eb-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="110eb-355">Rebuild DB</span></span> |<span data-ttu-id="110eb-356">Ricompilare database hello e caricarla con i dati di esempio team.</span><span class="sxs-lookup"><span data-stu-id="110eb-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="110eb-357">Edit / Details / Delete</span><span class="sxs-lookup"><span data-stu-id="110eb-357">Edit / Details / Delete</span></span> |<span data-ttu-id="110eb-358">Modifica un team, visualizza dettagli per un team, elimina un team.</span><span class="sxs-lookup"><span data-stu-id="110eb-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="110eb-359">Fare clic su alcune delle azioni hello e sperimentare il recupero dei dati di hello provenienti da origini diverse hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="110eb-360">Non hello le differenze nel tempo hello che necessario hello toocomplete diverse modalità di recupero dei dati hello dal database di hello e cache di hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="110eb-361">Eliminare le risorse di hello dopo aver terminato con un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="110eb-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="110eb-362">Quando si è terminato con un'applicazione hello esempio dell'esercitazione, è possibile eliminare hello Azure le risorse utilizzate in ordine tooconserve costi e le risorse.</span><span class="sxs-lookup"><span data-stu-id="110eb-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="110eb-363">Se si utilizza hello **distribuire tooAzure** pulsante hello [hello di effettuare il provisioning delle risorse di Azure](#provision-the-azure-resources) sezione e tutte le risorse sono contenute in hello stesso gruppo di risorse, è possibile eliminarle insieme in uno operazione eliminando il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="110eb-364">Accedi toohello [portale di Azure](https://portal.azure.com) e fare clic su **gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="110eb-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="110eb-365">Nome del gruppo di risorse in hello hello di tipo **filtrare gli elementi...**  casella di testo.</span><span class="sxs-lookup"><span data-stu-id="110eb-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="110eb-366">Fare clic su **...**  toohello a destra del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="110eb-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="110eb-367">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="110eb-367">Click **Delete**.</span></span>
   
    ![Elimina][cache-delete-resource-group]
5. <span data-ttu-id="110eb-369">Nome del gruppo di risorse e fare clic su di tipo hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="110eb-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Conferma dell'eliminazione][cache-delete-confirm]

<span data-ttu-id="110eb-371">Dopo la risorsa di hello pochi istanti gruppo e tutte le risorse indipendenti vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="110eb-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="110eb-372">Si noti che l'eliminazione di un gruppo di risorse è irreversibile e il gruppo di risorse di hello e tutte le risorse di hello in essa contenuti vengono eliminate definitivamente.</span><span class="sxs-lookup"><span data-stu-id="110eb-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="110eb-373">Assicurarsi che non si accidentalmente Elimina il gruppo di risorse non corretto di hello o risorse.</span><span class="sxs-lookup"><span data-stu-id="110eb-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="110eb-374">Se è stato creato risorse hello per l'hosting in questo esempio all'interno di un gruppo di risorse esistente, è possibile eliminare singolarmente ogni risorsa da loro rispettivi pannelli.</span><span class="sxs-lookup"><span data-stu-id="110eb-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="110eb-375">Eseguire l'applicazione di esempio hello sul computer locale</span><span class="sxs-lookup"><span data-stu-id="110eb-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="110eb-376">un'applicazione hello toorun localmente nel computer, è necessario una Cache Redis di Azure dell'istanza in cui toocache i dati.</span><span class="sxs-lookup"><span data-stu-id="110eb-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="110eb-377">Se è stata pubblicata l'applicazione tooAzure come descritto nella sezione precedente di hello, è possibile utilizzare l'istanza di Cache Redis di Azure hello che è stato eseguito il provisioning durante questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="110eb-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="110eb-378">Se si dispone di un'altra istanza di Cache Redis di Azure esistente, è possibile utilizzare tale toorun in questo esempio in locale.</span><span class="sxs-lookup"><span data-stu-id="110eb-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="110eb-379">Se è necessario toocreate un'istanza di Cache Redis di Azure, è possibile seguire i passaggi di hello in [creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="110eb-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="110eb-380">Dopo aver selezionato o creato toouse cache di hello, esplorare toohello cache nel portale di Azure hello e recuperare hello [nome host](cache-configure.md#properties) e [le chiavi di accesso](cache-configure.md#access-keys) per la cache.</span><span class="sxs-lookup"><span data-stu-id="110eb-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="110eb-381">Per istruzioni, vedere [Configurare le impostazioni della cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="110eb-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="110eb-382">Aprire hello `WebAppPlusCacheAppSecrets.config` file creati durante hello [configurare toouse applicazione hello Cache Redis](#configure-the-application-to-use-redis-cache) passaggio di questa esercitazione utilizzando editor hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="110eb-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="110eb-383">Modifica hello `value` attributo e sostituire `MyCache.redis.cache.windows.net` con hello [nome host](cache-configure.md#properties) della cache e specificare entrambi hello [chiave primaria o secondaria](cache-configure.md#access-keys) della cache come password hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="110eb-384">Premere **Ctrl + F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="110eb-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="110eb-385">Si noti che cache di hello perché un'applicazione hello, tra cui database hello, viene eseguito localmente e hello Cache Redis è ospitata in Azure, ammesso toounder-hello dei database.</span><span class="sxs-lookup"><span data-stu-id="110eb-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="110eb-386">Per prestazioni ottimali, hello applicazione client e l'istanza di Cache Redis di Azure deve essere in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="110eb-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="110eb-387">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="110eb-387">Next steps</span></span>
* <span data-ttu-id="110eb-388">Altre informazioni, vedere [Introduzione a ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) su hello [ASP.NET](http://asp.net/) sito.</span><span class="sxs-lookup"><span data-stu-id="110eb-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="110eb-389">Per ulteriori esempi di creazione di un'App Web ASP.NET nel servizio App, vedere [creare e distribuire un'app web ASP.NET in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) da hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connetti [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="110eb-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="110eb-390">Per altre guide rapide dalla demo HealthClinic.biz hello, vedere [strumenti Guida introduttiva per sviluppatori di Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="110eb-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="110eb-391">Altre informazioni su hello [codice prima tooa nuovo database](https://msdn.microsoft.com/data/jj193542) approccio tooEntity Framework che viene utilizzato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="110eb-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="110eb-392">Altre informazioni sulle [app Web nel servizio app di Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="110eb-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="110eb-393">Informazioni su come troppo[monitoraggio](cache-how-to-monitor.md) la cache di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="110eb-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="110eb-394">Esplorare le funzionalità Premium della cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="110eb-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="110eb-395">Come la persistenza tooconfigure per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="110eb-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="110eb-396">Come tooconfigure clustering per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="110eb-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="110eb-397">La modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="110eb-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="110eb-398">Vedere hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) per ulteriori informazioni sulle dimensioni, velocità effettiva e la larghezza di banda con cache premium.</span><span class="sxs-lookup"><span data-stu-id="110eb-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

