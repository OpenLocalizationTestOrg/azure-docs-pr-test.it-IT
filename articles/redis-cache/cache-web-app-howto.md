---
title: Come creare un'app Web con la cache Redis | Microsoft Docs
description: Informazioni su come creare un'app Web con la cache Redis
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="394bc-103">Come creare un'app Web con la cache Redis</span><span class="sxs-lookup"><span data-stu-id="394bc-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="394bc-104">.NET</span><span class="sxs-lookup"><span data-stu-id="394bc-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="394bc-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="394bc-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="394bc-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="394bc-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="394bc-107">Java</span><span class="sxs-lookup"><span data-stu-id="394bc-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="394bc-108">Python</span><span class="sxs-lookup"><span data-stu-id="394bc-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="394bc-109">Questa esercitazione illustra come creare e distribuire un'applicazione Web ASP.NET in un'app Web nel servizio app di Azure usando Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="394bc-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="394bc-110">L'applicazione di esempio mostra un elenco di statistiche del team da un database e illustra i diversi modi in cui è possibile usare la cache Redis di Azure per archiviare e recuperare i dati dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="394bc-111">Al termine dell'esercitazione, si avrà un'app Web in esecuzione che legge e scrive in un database, ottimizzata per la cache Redis di Azure e ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="394bc-112">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="394bc-112">You'll learn:</span></span>

* <span data-ttu-id="394bc-113">Come creare un'applicazione Web ASP.NET MVC 5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="394bc-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="394bc-114">Come accedere ai dati da un database usando Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="394bc-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="394bc-115">Come ottimizzare la velocità effettiva dei dati e ridurre il carico del database archiviando e recuperando i dati con la cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="394bc-116">Come usare un set ordinato Redis per recuperare i primi 5 team.</span><span class="sxs-lookup"><span data-stu-id="394bc-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="394bc-117">Come effettuare il provisioning delle risorse di Azure per l'applicazione usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="394bc-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="394bc-118">Come pubblicare l'applicazione in Azure usando Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="394bc-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="394bc-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="394bc-119">Prerequisites</span></span>
<span data-ttu-id="394bc-120">Per completare l'esercitazione, sono necessari i prerequisiti seguenti.</span><span class="sxs-lookup"><span data-stu-id="394bc-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="394bc-121">Account di Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="394bc-122">Visual Studio 2017 con Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="394bc-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="394bc-123">Account Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-123">Azure account</span></span>
<span data-ttu-id="394bc-124">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="394bc-125">È possibile:</span><span class="sxs-lookup"><span data-stu-id="394bc-125">You can:</span></span>

* <span data-ttu-id="394bc-126">[Aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero):</span><span class="sxs-lookup"><span data-stu-id="394bc-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="394bc-127">sono inclusi crediti da usare per provare i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="394bc-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="394bc-128">Una volta esauriti i crediti, è possibile mantenere l'account e usare le funzionalità e i servizi di Azure gratuiti.</span><span class="sxs-lookup"><span data-stu-id="394bc-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="394bc-129">[Attivare i vantaggi della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="394bc-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="394bc-130">con l'abbonamento MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="394bc-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="394bc-131">Visual Studio 2017 con Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="394bc-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="394bc-132">L'esercitazione è stata scritta per Visual Studio 2017 con [Azure SDK per .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="394bc-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="394bc-133">Azure SDK 2.9.5 è incluso nel programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="394bc-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="394bc-134">Se è installato Visual Studio 2015, è possibile seguire l'esercitazione con [Azure SDK per .NET](../dotnet-sdk.md) 2.8.2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="394bc-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="394bc-135">[Scaricare qui la versione più recente di Azure SDK per Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="394bc-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="394bc-136">Visual Studio viene installato automaticamente con l'SDK, se necessario.</span><span class="sxs-lookup"><span data-stu-id="394bc-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="394bc-137">Alcune schermate potrebbero essere diverse da quelle illustrate nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="394bc-138">Se è disponibile Visual Studio 2013, è possibile [scaricare la versione più recente di Azure SDK per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="394bc-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="394bc-139">Alcune schermate potrebbero essere diverse da quelle illustrate nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="394bc-140">Creare il progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="394bc-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="394bc-141">Aprire Visual Studio e fare clic su **File**, **Nuovo**, **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="394bc-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="394bc-142">Espandere il nodo **Visual C#** nell'elenco **Modelli**, selezionare **Cloud** e fare clic su **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="394bc-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="394bc-143">Assicurarsi che sia selezionata l'opzione **.NET Framework 4.5.2** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="394bc-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="394bc-144">Immettere **ContosoTeamStats** nella casella di testo **Nome** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="394bc-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Crea progetto][cache-create-project]
3. <span data-ttu-id="394bc-146">Selezionare **MVC** come tipo di progetto.</span><span class="sxs-lookup"><span data-stu-id="394bc-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="394bc-147">Assicurarsi che per l'impostazione **Autenticazione** sia specificato **Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="394bc-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="394bc-148">A seconda della versione di Visual Studio, il valore predefinito può essere diverso.</span><span class="sxs-lookup"><span data-stu-id="394bc-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="394bc-149">Per modificarlo, fare clic su **Modifica autenticazione** e selezionare **Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="394bc-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="394bc-150">Se si usa Visual Studio 2015, deselezionare la casella di controllo **Ospita nel cloud**.</span><span class="sxs-lookup"><span data-stu-id="394bc-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="394bc-151">Nei passaggi successivi dell'esercitazione si [effettuerà il provisioning delle risorse di Azure](#provision-the-azure-resources) e si [pubblicherà l'applicazione in Azure](#publish-the-application-to-azure).</span><span class="sxs-lookup"><span data-stu-id="394bc-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="394bc-152">Per un esempio di provisioning di un'app Web del servizio app da Visual Studio con l'opzione **Ospita nel cloud** selezionata, vedere [Introduzione alle app Web nel servizio app di Azure con ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="394bc-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Seleziona modello progetto][cache-select-template]
4. <span data-ttu-id="394bc-154">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="394bc-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="394bc-155">Creare l'applicazione ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="394bc-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="394bc-156">In questa sezione dell'esercitazione verrà creata l'applicazione di base che legge e visualizza le statistiche del team da un database.</span><span class="sxs-lookup"><span data-stu-id="394bc-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="394bc-157">Aggiungere il pacchetto NuGet di Entity Framework</span><span class="sxs-lookup"><span data-stu-id="394bc-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="394bc-158">Aggiungere il modello</span><span class="sxs-lookup"><span data-stu-id="394bc-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="394bc-159">Aggiungere il controller</span><span class="sxs-lookup"><span data-stu-id="394bc-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="394bc-160">Configurare le visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="394bc-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="394bc-161">Aggiungere il pacchetto NuGet di Entity Framework</span><span class="sxs-lookup"><span data-stu-id="394bc-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="394bc-162">Nel menu **Strumenti** fare clic su **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="394bc-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="394bc-163">Nella finestra **Console di Gestione pacchetti** eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="394bc-164">Per altre informazioni sul pacchetto, vedere la pagina NuGet relativa a [Entity Framework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="394bc-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="394bc-165">Aggiungere il modello</span><span class="sxs-lookup"><span data-stu-id="394bc-165">Add the model</span></span>
1. <span data-ttu-id="394bc-166">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="394bc-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Aggiungi modello][cache-model-add-class]
2. <span data-ttu-id="394bc-168">Immettere `Team` come nome della classe e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="394bc-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Aggiunta di una classe modello][cache-model-add-class-dialog]
3. <span data-ttu-id="394bc-170">Sostituire le istruzioni `using` all'inizio del file `Team.cs` con le istruzioni `using` seguenti.</span><span class="sxs-lookup"><span data-stu-id="394bc-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="394bc-171">Sostituire la definizione della classe `Team` con il frammento di codice seguente che contiene una classe `Team` aggiornata, oltre ad altre classi helper di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="394bc-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="394bc-172">Per altre informazioni sull'approccio Code First per Entity Framework usato in questa esercitazione, vedere [Code First per un nuovo database](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="394bc-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="394bc-173">In **Esplora soluzioni** fare doppio clic su **web.config** per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="394bc-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="394bc-175">Aggiungere la sezione `connectionStrings` riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="394bc-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="394bc-176">Il nome della stringa di connessione deve corrispondere al nome della classe contesto del database Entity Framework, ovvero `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="394bc-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="394bc-177">È possibile aggiungere la nuova sezione `connectionStrings` in modo che segua `configSections`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="394bc-178">La stringa di connessione potrebbe essere diversa a seconda della versione di Visual Studio e SQL Server Express Edition usate per completare l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="394bc-179">Il modello di web.config deve essere configurato in modo da corrispondere all'installazione e può contenere voci `Data Source` come `(LocalDB)\v11.0` da SQL Server Express 2012 o `Data Source=(LocalDB)\MSSQLLocalDB` da SQL Server Express 2014 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="394bc-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="394bc-180">Per altre informazioni sulle stringhe di connessione e le versioni di SQL Express, vedere [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="394bc-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="394bc-181">Aggiungere il controller</span><span class="sxs-lookup"><span data-stu-id="394bc-181">Add the controller</span></span>
1. <span data-ttu-id="394bc-182">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="394bc-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="394bc-183">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Controller**, quindi scegliere **Aggiungi**, **Controller**.</span><span class="sxs-lookup"><span data-stu-id="394bc-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Aggiungi controller][cache-add-controller]
3. <span data-ttu-id="394bc-185">Scegliere **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="394bc-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="394bc-186">Se viene visualizzato un errore dopo la selezione di **Aggiungi**, assicurarsi prima di tutto di avere compilato il progetto.</span><span class="sxs-lookup"><span data-stu-id="394bc-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Aggiunta di una classe controller][cache-add-controller-class]
4. <span data-ttu-id="394bc-188">Selezionare **Team (ContosoTeamStats.Models)** dall'elenco a discesa **Classe modello**.</span><span class="sxs-lookup"><span data-stu-id="394bc-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="394bc-189">Selezionare **TeamContext (ContosoTeamStats.Models)** dall'elenco a discesa **Classe del contesto dei dati**.</span><span class="sxs-lookup"><span data-stu-id="394bc-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="394bc-190">Immettere `TeamsController` nella casella di testo **Nome controller** , se non è stata popolata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="394bc-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="394bc-191">Fare clic su **Aggiungi** per creare la classe controller e aggiungere le visualizzazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="394bc-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Configura controller][cache-configure-controller]
5. <span data-ttu-id="394bc-193">In **Esplora soluzioni** espandere **Global.asax** e fare doppio clic su **Global.asax.cs** per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="394bc-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="394bc-195">Aggiungere le due istruzioni `using` seguenti all'inizio del file, dopo le altre due istruzioni `using`.</span><span class="sxs-lookup"><span data-stu-id="394bc-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="394bc-196">Aggiungere la riga di codice seguente alla fine del metodo `Application_Start` .</span><span class="sxs-lookup"><span data-stu-id="394bc-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="394bc-197">In **Esplora soluzioni** espandere `App_Start` e fare doppio clic su `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="394bc-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="394bc-199">Sostituire `controller = "Home"` nel codice seguente nel metodo `RegisterRoutes` con `controller = "Teams"`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="394bc-200">Configurare le visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="394bc-200">Configure the views</span></span>
1. <span data-ttu-id="394bc-201">In **Esplora soluzioni** espandere la cartella **Visualizzazioni**, quindi la cartella **Condiviso** e infine fare doppio clic su **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="394bc-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![file _Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="394bc-203">Cambiare il contenuto dell'elemento `title` e sostituire `My ASP.NET Application` con `Contoso Team Stats`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="394bc-204">Nella sezione `body` aggiornare la prima istruzione `Html.ActionLink` e sostituire `Application name` con `Contoso Team Stats`, quindi sostituire `Home` con `Teams`.</span><span class="sxs-lookup"><span data-stu-id="394bc-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="394bc-205">Prima: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="394bc-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="394bc-206">Dopo: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="394bc-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Modifiche al codice][cache-layout-cshtml-code]
2. <span data-ttu-id="394bc-208">Premere **CTRL+F5** per compilare ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="394bc-209">Questa versione dell'applicazione legge i risultati direttamente dal database.</span><span class="sxs-lookup"><span data-stu-id="394bc-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="394bc-210">Si notino le azioni **Crea nuovo**, **Modifica**, **Dettagli** ed **Elimina** aggiunte automaticamente all'applicazione dallo scaffolding **Controller MVC 5 con visualizzazioni, che usa Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="394bc-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="394bc-211">Nella sezione successiva dell'esercitazione verrà aggiunta la cache Redis, per ottimizzare l'accesso ai dati e fornire funzionalità aggiuntive all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Applicazione iniziale][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="394bc-213">Configurare l'applicazione per l'uso della cache Redis</span><span class="sxs-lookup"><span data-stu-id="394bc-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="394bc-214">In questa sezione dell'esercitazione verrà configurata l'applicazione di esempio per archiviare e recuperare le statistiche del team Contoso da un'istanza della cache Redis di Azure usando il client [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) della cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="394bc-215">Configurare l'applicazione per l'uso di StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="394bc-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="394bc-216">Aggiornare la classe TeamsController per restituire risultati dalla cache o dal database</span><span class="sxs-lookup"><span data-stu-id="394bc-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="394bc-217">Aggiornare i metodi Create, Edit e Delete per l'interazione con la cache</span><span class="sxs-lookup"><span data-stu-id="394bc-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="394bc-218">Aggiornare la visualizzazione Index dei team per l'interazione con la cache</span><span class="sxs-lookup"><span data-stu-id="394bc-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="394bc-219">Configurare l'applicazione per l'uso di StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="394bc-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="394bc-220">Per configurare un'applicazione client in Visual Studio con il pacchetto NuGet StackExchange.Redis, fare clic su **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti** dal menu **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="394bc-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="394bc-221">Eseguire questo comando seguente dalla finestra `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="394bc-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="394bc-222">Il pacchetto NuGet scarica e aggiunge i riferimenti ad assembly necessari per consentire all'applicazione client di accedere a Cache Redis di Azure con il client della cache StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="394bc-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="394bc-223">Se si preferisce usare una versione con nome sicuro della libreria client `StackExchange.Redis`, installare il pacchetto `StackExchange.Redis.StrongName`.</span><span class="sxs-lookup"><span data-stu-id="394bc-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="394bc-224">In **Esplora soluzioni** espandere la cartella **Controller** e fare doppio clic su **TeamsController.cs** per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="394bc-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Controller Teams][cache-teamscontroller]
4. <span data-ttu-id="394bc-226">Aggiungere le due istruzioni `using` seguenti a **TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="394bc-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="394bc-227">Aggiungere le due proprietà seguenti alla classe `TeamsController` .</span><span class="sxs-lookup"><span data-stu-id="394bc-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="394bc-228">Creare un file nel computer denominato `WebAppPlusCacheAppSecrets.config` e inserirlo in una posizione che non verrà archiviata con il codice sorgente dell'applicazione di esempio, nel caso in cui si decidesse di archiviarlo.</span><span class="sxs-lookup"><span data-stu-id="394bc-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="394bc-229">In questo esempio il file `AppSettingsSecrets.config` si trova in `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="394bc-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="394bc-230">Modificare il file `WebAppPlusCacheAppSecrets.config` e aggiungere il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="394bc-231">Se si esegue localmente l'applicazione, queste informazioni vengono usate per connettersi all'istanza della cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="394bc-232">Successivamente nell'esercitazione verrà effettuato il provisioning di un'istanza della cache Redis di Azure e verranno aggiornati il nome e la password della cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="394bc-233">Se non si prevede di eseguire localmente l'applicazione di esempio, è possibile ignorare la creazione di questo file e i passaggi successivi che fanno riferimento al file, perché, quando si esegue la distribuzione in Azure, l'applicazione recupera le informazioni di connessione della cache dall'impostazione dell'app per l'app Web, non da questo file.</span><span class="sxs-lookup"><span data-stu-id="394bc-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="394bc-234">Poiché `WebAppPlusCacheAppSecrets.config` non viene distribuito in Azure con l'applicazione, sarà necessario solo se si esegue l'applicazione localmente.</span><span class="sxs-lookup"><span data-stu-id="394bc-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="394bc-235">In **Esplora soluzioni** fare doppio clic su **web.config** per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="394bc-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="394bc-237">Aggiungere l'attributo `file` seguente all'elemento `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="394bc-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="394bc-238">Se è stato usato un nome o un percorso di file diverso, sostituire i valori dell'esempio con questi valori.</span><span class="sxs-lookup"><span data-stu-id="394bc-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="394bc-239">Prima: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="394bc-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="394bc-240">Dopo: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="394bc-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="394bc-241">Il runtime ASP.NET unisce il contenuto del file esterno con il markup nell'elemento `<appSettings>` .</span><span class="sxs-lookup"><span data-stu-id="394bc-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="394bc-242">Il runtime ignora l'attributo del file, se non è possibile trovare il file specificato.</span><span class="sxs-lookup"><span data-stu-id="394bc-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="394bc-243">I segreti, ovvero la stringa di connessione per la cache, non sono inclusi come parte del codice sorgente per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="394bc-244">Quando si distribuisce l'app Web in Azure, il file `WebAppPlusCacheAppSecrests.config` non verrà distribuito (approccio consigliato).</span><span class="sxs-lookup"><span data-stu-id="394bc-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="394bc-245">È possibile specificare in molti modi questi segreti in Azure e in questa esercitazione vengono configurati automaticamente quando si effettua il [provisioning delle risorse di Azure](#provision-the-azure-resources) in un passaggio successivo dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="394bc-246">Per altre informazioni sull'uso dei segreti in Azure, vedere l'articolo [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)(Procedure consigliate per la distribuzione di password e altri dati sensibili in ASP.NET e nel servizio app di Azure).</span><span class="sxs-lookup"><span data-stu-id="394bc-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="394bc-247">Aggiornare la classe TeamsController per restituire risultati dalla cache o dal database</span><span class="sxs-lookup"><span data-stu-id="394bc-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="394bc-248">In questo esempio è possibile recuperare le statistiche del team dal database o dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="394bc-249">Le statistiche del team vengono archiviate nella cache come elemento `List<Team>`serializzato e anche come set ordinato usando tipi di dati Redis.</span><span class="sxs-lookup"><span data-stu-id="394bc-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="394bc-250">Quando si recuperano elementi da un set ordinato, è possibile recuperare alcuni o tutti gli elementi o eseguire query per determinati elementi.</span><span class="sxs-lookup"><span data-stu-id="394bc-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="394bc-251">In questo esempio verrà eseguita una query sul set ordinato per i primi cinque team classificati in base al numero di vittorie.</span><span class="sxs-lookup"><span data-stu-id="394bc-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="394bc-252">Per usare la cache Redis di Azure, non è necessario archiviare le statistiche del team in più formati nella cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="394bc-253">Questa esercitazione usa più formati per illustrare alcuni dei modi diversi e dei tipi di dati diversi che è possibile usare per memorizzare i dati nella cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="394bc-254">Aggiungere le istruzioni `using` seguenti nella parte iniziale del file `TeamsController.cs`, insieme alle altre istruzioni `using`.</span><span class="sxs-lookup"><span data-stu-id="394bc-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="394bc-255">Sostituire l'implementazione del metodo `public ActionResult Index()` corrente con l'implementazione seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="394bc-256">Aggiungere i tre metodi seguenti alla classe `TeamsController` per implementare i tipi di azione `playGames`, `clearCache` e `rebuildDB` dall'istruzione switch aggiunta nel frammento di codice precedente.</span><span class="sxs-lookup"><span data-stu-id="394bc-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="394bc-257">Il metodo `PlayGames` aggiorna le statistiche del team simulando una stagione di partite, salva i risultati nel database e cancella i dati ora obsoleti dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="394bc-258">Il metodo `RebuildDB` inizializza di nuovo il database con il set predefinito di team, genera le rispettive statistiche e cancella i dati ora obsoleti dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="394bc-259">Il metodo `ClearCachedTeams` rimuove dalla cache eventuali statistiche del team memorizzate.</span><span class="sxs-lookup"><span data-stu-id="394bc-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="394bc-260">Aggiungere i quattro metodi seguenti alla classe `TeamsController` per implementare diversi modi di recupero per le statistiche del team dalla cache e dal database.</span><span class="sxs-lookup"><span data-stu-id="394bc-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="394bc-261">Ogni metodo restituisce un valore `List<Team>` , che viene quindi mostrato nella visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="394bc-262">Il metodo `GetFromDB` legge le statistiche del team dal database.</span><span class="sxs-lookup"><span data-stu-id="394bc-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="394bc-263">Il metodo `GetFromList` legge le statistiche del team dalla cache, come elemento `List<Team>` serializzato.</span><span class="sxs-lookup"><span data-stu-id="394bc-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="394bc-264">In caso di mancato riscontro nella cache, le statistiche del team vengono lette dal database e quindi archiviate nella cache per la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="394bc-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="394bc-265">In questo esempio viene usata la serializzazione JSON.NET per serializzare gli oggetti .NET verso e dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="394bc-266">Per altre informazioni, vedere [Come usare gli oggetti .NET nella cache Redis di Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="394bc-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="394bc-267">Il metodo `GetFromSortedSet` legge le statistiche del team da un set ordinato memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="394bc-268">In caso di mancato riscontro nella cache, le statistiche del team vengono lette dal database e archiviate nella cache come set ordinato.</span><span class="sxs-lookup"><span data-stu-id="394bc-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="394bc-269">Il metodo `GetFromSortedSetTop5` legge i primi cinque team dal set ordinato memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="394bc-270">Controlla prima di tutto la cache per verificare l'esistenza della chiave `teamsSortedSet` .</span><span class="sxs-lookup"><span data-stu-id="394bc-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="394bc-271">Se la chiave non è presente, viene chiamato il metodo `GetFromSortedSet` per leggere le statistiche del team e archiviarle nella cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="394bc-272">Il set ordinato memorizzato nella cache viene quindi sottoposto a query alla ricerca dei primi cinque team, che vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="394bc-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="394bc-273">Aggiornare i metodi Create, Edit e Delete per l'interazione con la cache</span><span class="sxs-lookup"><span data-stu-id="394bc-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="394bc-274">Il codice di scaffolding generato come parte di questo esempio include metodi per l'aggiunta, la modifica e l'eliminazione di elementi.</span><span class="sxs-lookup"><span data-stu-id="394bc-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="394bc-275">Quando un team viene aggiunto, modificato o rimosso, i dati nella cache diventano obsoleti.</span><span class="sxs-lookup"><span data-stu-id="394bc-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="394bc-276">In questa sezione verranno modificati questi tre metodi per cancellare i team memorizzati nella cache, in modo che la cache non risulti non sincronizzata con il database.</span><span class="sxs-lookup"><span data-stu-id="394bc-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="394bc-277">Passare al metodo `Create(Team team)` nella classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="394bc-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="394bc-278">Aggiungere una chiamata al metodo `ClearCachedTeams` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="394bc-279">Passare al metodo `Edit(Team team)` nella classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="394bc-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="394bc-280">Aggiungere una chiamata al metodo `ClearCachedTeams` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="394bc-281">Passare al metodo `DeleteConfirmed(int id)` nella classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="394bc-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="394bc-282">Aggiungere una chiamata al metodo `ClearCachedTeams` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="394bc-283">Aggiornare la visualizzazione Index dei team per l'interazione con la cache</span><span class="sxs-lookup"><span data-stu-id="394bc-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="394bc-284">In **Esplora soluzioni** espandere la cartella **Visualizzazioni**, quindi la cartella **Team** e fare doppio clic su **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="394bc-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="394bc-286">Cercare l'elemento paragrafo seguente nella parte superiore del file.</span><span class="sxs-lookup"><span data-stu-id="394bc-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Tabella delle azioni][cache-teams-index-table]
   
    <span data-ttu-id="394bc-288">Questo è il collegamento per la creazione di un nuovo team.</span><span class="sxs-lookup"><span data-stu-id="394bc-288">This is the link to create a new team.</span></span> <span data-ttu-id="394bc-289">Sostituire l'elemento paragrafo con la tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="394bc-290">Questa tabella include collegamenti alle azioni per la creazione di un nuovo team, l'avvio di una nuova stagione di partite, la cancellazione della cache, il recupero dei team dalla cache in diversi formati, il recupero di team dal database e la ricompilazione del database con dati di esempio aggiornati.</span><span class="sxs-lookup"><span data-stu-id="394bc-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="394bc-291">Passare alla parte finale del file **Index.cshtml** e aggiungere l'elemento `tr` seguente, in modo che costituisca l'ultima riga dell'ultima tabella del file.</span><span class="sxs-lookup"><span data-stu-id="394bc-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="394bc-292">Questa riga mostra il valore di `ViewBag.Msg` che contiene un rapporto sullo stato relativo all'operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="394bc-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="394bc-293">`ViewBag.Msg` viene impostato quando si fa clic su uno dei collegamenti all'azione del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="394bc-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Messaggio di stato][cache-status-message]
2. <span data-ttu-id="394bc-295">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="394bc-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="394bc-296">provisioning delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-296">Provision the Azure resources</span></span>
<span data-ttu-id="394bc-297">Per ospitare l'applicazione in Azure, è prima di tutto necessario effettuare il provisioning dei servizi di Azure richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="394bc-298">L'applicazione di esempio di questa esercitazione usa i servizi di Azure seguenti.</span><span class="sxs-lookup"><span data-stu-id="394bc-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="394bc-299">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-299">Azure Redis Cache</span></span>
* <span data-ttu-id="394bc-300">App Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="394bc-300">App Service Web App</span></span>
* <span data-ttu-id="394bc-301">Database SQL</span><span class="sxs-lookup"><span data-stu-id="394bc-301">SQL Database</span></span>

<span data-ttu-id="394bc-302">Per distribuire questi servizi in un gruppo di risorse nuovo o esistente, fare clic sul pulsante **Distribuisci in Azure** seguente.</span><span class="sxs-lookup"><span data-stu-id="394bc-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="394bc-303">[![Distribuisci in Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="394bc-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="394bc-304">Il pulsante **Distribuisci in Azure** usa il modello per [creare un'app Web con cache Redis e database SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) di [Avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates) per effettuare il provisioning di questi servizi e configurare la stringa di connessione per il database SQL e l'impostazione dell'applicazione per la stringa di connessione della cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="394bc-305">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="394bc-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="394bc-306">Se si fa clic sul pulsante **Distribuisci in Azure** , verrà aperto il portale di Azure e verrà avviato il processo di creazione delle risorse descritte dal modello.</span><span class="sxs-lookup"><span data-stu-id="394bc-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Distribuzione in Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="394bc-308">Nella sezione **Informazioni di base** selezionare la sottoscrizione di Azure da usare, quindi selezionare un gruppo di risorse esistente o crearne uno nuovo e infine specificare la posizione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="394bc-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="394bc-309">Nella sezione **Impostazioni** specificare un **account di accesso amministratore** diverso da **admin**, la **password di accesso dell'amministratore** e il **nome del database**.</span><span class="sxs-lookup"><span data-stu-id="394bc-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="394bc-310">Gli altri parametri vengono configurati per un piano di hosting del Servizio app gratuito e per i piani con opzioni di costo inferiori per il database SQL e la Cache Redis di Azure, non disponibili con un livello gratuito.</span><span class="sxs-lookup"><span data-stu-id="394bc-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Distribuzione in Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="394bc-312">Dopo avere configurato le impostazioni desiderate, scorrere fino alla fine della pagina, leggere i termini e le condizioni e selezionare la casella di controllo **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="394bc-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="394bc-313">Per iniziare il provisioning delle risorse, fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="394bc-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="394bc-314">Per visualizzare lo stato della distribuzione, fare clic sull'icona di notifica e quindi su **La distribuzione è stata avviata**.</span><span class="sxs-lookup"><span data-stu-id="394bc-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![La distribuzione è stata avviata][cache-deployment-started]

<span data-ttu-id="394bc-316">È possibile visualizzare lo stato della distribuzione nel pannello **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="394bc-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Distribuisci in Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="394bc-318">Al termine del provisioning, è possibile pubblicare l'applicazione in Azure da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="394bc-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="394bc-319">Eventuali errori durante il processo di provisioning vengono visualizzati nel pannello **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="394bc-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="394bc-320">Gli errori comuni sono relativi a un numero eccessivo di server SQL o di piani di hosting del Servizio app gratuito per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="394bc-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="394bc-321">Risolvere eventuali errori e riavviare il processo facendo clic su **Ridistribuisci** nel pannello **Microsoft.Template** o sul pulsante **Distribuisci in Azure** in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="394bc-322">Pubblicare l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-322">Publish the application to Azure</span></span>
<span data-ttu-id="394bc-323">In questo passaggio dell'esercitazione l'applicazione verrà pubblicata in Azure e verrà eseguita sul cloud.</span><span class="sxs-lookup"><span data-stu-id="394bc-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="394bc-324">Fare clic con il pulsante destro del mouse sul progetto **ContosoTeamStats** in Visual Studio e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="394bc-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Pubblica][cache-publish-app]
2. <span data-ttu-id="394bc-326">Fare clic su **Servizio app di Microsoft Azure**, scegliere **Seleziona esistente** e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="394bc-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Pubblica][cache-publish-to-app-service]
3. <span data-ttu-id="394bc-328">Selezionare la sottoscrizione usata durante la creazione delle risorse di Azure, espandere il gruppo di risorse contenente le risorse e scegliere l'app Web da usare.</span><span class="sxs-lookup"><span data-stu-id="394bc-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="394bc-329">Se è stato usato il pulsante **Distribuisci in Azure**, il nome dell'app Web inizierà con **webSite**, seguito da caratteri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="394bc-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Selezione dell'app Web][cache-select-web-app]
4. <span data-ttu-id="394bc-331">Fare clic su **OK** per iniziare il processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="394bc-332">Il processo di pubblicazione viene completato in pochi minuti e viene aperto un browser con l'applicazione di esempio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="394bc-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="394bc-333">Se viene visualizzato un errore DNS durante la convalida o la pubblicazione e il processo di provisioning per le risorse di Azure per l'applicazione è stato completato di recente, attendere qualche minuto e riprovare.</span><span class="sxs-lookup"><span data-stu-id="394bc-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache aggiunta][cache-added-to-application]

<span data-ttu-id="394bc-335">La tabella seguente illustra ogni collegamento all'azione dall'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="394bc-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="394bc-336">Azione</span><span class="sxs-lookup"><span data-stu-id="394bc-336">Action</span></span> | <span data-ttu-id="394bc-337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="394bc-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="394bc-338">Creazione di un nuovo sito</span><span class="sxs-lookup"><span data-stu-id="394bc-338">Create New</span></span> |<span data-ttu-id="394bc-339">Crea un nuovo team.</span><span class="sxs-lookup"><span data-stu-id="394bc-339">Create a new Team.</span></span> |
| <span data-ttu-id="394bc-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="394bc-340">Play Season</span></span> |<span data-ttu-id="394bc-341">Avvia una stagione di partite, aggiorna le statistiche del team e cancella eventuali dati del team obsoleti dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="394bc-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="394bc-342">Clear Cache</span></span> |<span data-ttu-id="394bc-343">Cancella le statistiche del team dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="394bc-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="394bc-344">List from Cache</span></span> |<span data-ttu-id="394bc-345">Recupera le statistiche del team dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="394bc-346">In caso di mancato riscontro nella cache, carica le statistiche dal database e le salva nella cache per la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="394bc-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="394bc-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="394bc-347">Sorted Set from Cache</span></span> |<span data-ttu-id="394bc-348">Recupera le statistiche del team dalla cache usando un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="394bc-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="394bc-349">In caso di mancato riscontro nella cache, carica le statistiche dal database e le salva nella cache mediante un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="394bc-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="394bc-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="394bc-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="394bc-351">Recupera i primi cinque team dalla cache usando un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="394bc-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="394bc-352">In caso di mancato riscontro nella cache, carica le statistiche dal database e le salva nella cache mediante un set ordinato.</span><span class="sxs-lookup"><span data-stu-id="394bc-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="394bc-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="394bc-353">Load from DB</span></span> |<span data-ttu-id="394bc-354">Recupera le statistiche del team dal database.</span><span class="sxs-lookup"><span data-stu-id="394bc-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="394bc-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="394bc-355">Rebuild DB</span></span> |<span data-ttu-id="394bc-356">Ricompila il database e lo ricarica con i dati del team di esempio.</span><span class="sxs-lookup"><span data-stu-id="394bc-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="394bc-357">Edit / Details / Delete</span><span class="sxs-lookup"><span data-stu-id="394bc-357">Edit / Details / Delete</span></span> |<span data-ttu-id="394bc-358">Modifica un team, visualizza dettagli per un team, elimina un team.</span><span class="sxs-lookup"><span data-stu-id="394bc-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="394bc-359">Fare clic su alcune azioni e provare a recuperare i dati dalle diverse origini.</span><span class="sxs-lookup"><span data-stu-id="394bc-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="394bc-360">Notare le differenze a livello di tempo necessario per il completamento nelle varie modalità di recupero di dati dal database e dalla cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="394bc-361">Eliminare le risorse al termine dell'uso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="394bc-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="394bc-362">Al termine dell'uso dell'applicazione di esempio dell'esercitazione, è possibile eliminare le risorse di Azure per ridurre i costi e l'uso di risorse.</span><span class="sxs-lookup"><span data-stu-id="394bc-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="394bc-363">Se si usa il pulsante **Distribuisci in Azure** nella sezione [Effettuare il provisioning delle risorse di Azure](#provision-the-azure-resources) e se tutte le risorse sono contenute nello stesso gruppo di risorse, è possibile eliminarle tutte insieme in una sola operazione, eliminando il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="394bc-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="394bc-364">Accedere al [portale di Azure](https://portal.azure.com) e fare clic su **Gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="394bc-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="394bc-365">Immettere il nome del gruppo di risorse nella casella di testo **Filtra elementi** .</span><span class="sxs-lookup"><span data-stu-id="394bc-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="394bc-366">Fare clic su **...** a destra del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="394bc-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="394bc-367">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="394bc-367">Click **Delete**.</span></span>
   
    ![Elimina][cache-delete-resource-group]
5. <span data-ttu-id="394bc-369">Immettere il nome del gruppo di risorse e fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="394bc-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Conferma dell'eliminazione][cache-delete-confirm]

<span data-ttu-id="394bc-371">Dopo alcuni minuti il gruppo di risorse e tutte le risorse in esso contenute vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="394bc-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="394bc-372">Si noti che l'eliminazione di un gruppo di risorse è irreversibile e che il gruppo di risorse e tutte le risorse incluse nel gruppo vengono eliminati definitivamente.</span><span class="sxs-lookup"><span data-stu-id="394bc-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="394bc-373">Assicurarsi di non eliminare accidentalmente il gruppo di risorse sbagliato o le risorse errate.</span><span class="sxs-lookup"><span data-stu-id="394bc-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="394bc-374">Se le risorse per l'hosting di questo esempio sono state create in un gruppo di risorse esistente, è possibile eliminare singolarmente ogni risorsa dal rispettivo pannello.</span><span class="sxs-lookup"><span data-stu-id="394bc-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="394bc-375">Eseguire l'applicazione di esempio nel computer locale</span><span class="sxs-lookup"><span data-stu-id="394bc-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="394bc-376">Per eseguire l'applicazione localmente nel computer, è necessaria un'istanza della cache Redis di Azure in cui memorizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="394bc-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="394bc-377">Se l'applicazione è stata pubblicata in Azure come illustrato nella sezione precedente, è possibile usare l'istanza della cache Redis di Azure di cui è stato effettuato il provisioning in quel passaggio.</span><span class="sxs-lookup"><span data-stu-id="394bc-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="394bc-378">Se è disponibile un'altra istanza esistente della cache Redis di Azure, è possibile usarla per eseguire localmente questo esempio.</span><span class="sxs-lookup"><span data-stu-id="394bc-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="394bc-379">Se è necessario creare un'istanza della cache Redis di Azure, è possibile seguire la procedura illustrata in [Creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="394bc-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="394bc-380">Dopo la selezione o la creazione della cache da usare, passare alla cache nel portale di Azure e recuperare il [nome host](cache-configure.md#properties) e le [chiavi di accesso](cache-configure.md#access-keys) per la cache.</span><span class="sxs-lookup"><span data-stu-id="394bc-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="394bc-381">Per istruzioni, vedere [Configurare le impostazioni della cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="394bc-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="394bc-382">Aprire il file `WebAppPlusCacheAppSecrets.config` creato durante il passaggio [Configurare l'applicazione per l'uso della cache Redis](#configure-the-application-to-use-redis-cache) di questa esercitazione usando l'editor preferito.</span><span class="sxs-lookup"><span data-stu-id="394bc-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="394bc-383">Modificare l'attributo `value` e sostituire `MyCache.redis.cache.windows.net` con il [nome host](cache-configure.md#properties) della cache, quindi specificare la [chiave primaria o secondaria](cache-configure.md#access-keys) della cache come password.</span><span class="sxs-lookup"><span data-stu-id="394bc-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="394bc-384">Premere **CTRL+F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="394bc-385">Si noti che poiché l'applicazione, incluso il database, viene eseguita localmente e la Cache Redis è ospitata in Azure, è possibile che le prestazioni della cache risultino inferiori a quelle del database.</span><span class="sxs-lookup"><span data-stu-id="394bc-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="394bc-386">Per prestazioni ottimali, l'applicazione client e la cache Redis di Azure devono trovarsi nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="394bc-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="394bc-387">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="394bc-387">Next steps</span></span>
* <span data-ttu-id="394bc-388">Per altre informazioni, vedere [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) (Introduzione ad ASP.NET MVC 5) nel sito [ASP.NET](http://asp.net/).</span><span class="sxs-lookup"><span data-stu-id="394bc-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="394bc-389">Per altri esempi di creazione di un'app Web ASP.NET nel servizio app, vedere [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) (Creare e distribuire un'app Web ASP.NET nel sevizio app di Azure) per la [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) di Connect 2015.</span><span class="sxs-lookup"><span data-stu-id="394bc-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="394bc-390">Per altre guide introduttive della demo HealthClinic.biz, vedere [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)(Guide introduttive agli strumenti di sviluppo di Azure).</span><span class="sxs-lookup"><span data-stu-id="394bc-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="394bc-391">Altre informazioni sull'approccio [Code First per un nuovo database](https://msdn.microsoft.com/data/jj193542) per Entity Framework usato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="394bc-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="394bc-392">Altre informazioni sulle [app Web nel servizio app di Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="394bc-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="394bc-393">Altre informazioni sul [monitoraggio](cache-how-to-monitor.md) della cache nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="394bc-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="394bc-394">Esplorare le funzionalità Premium della cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="394bc-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="394bc-395">Come configurare la persistenza per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="394bc-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="394bc-396">Come configurare il servizio cluster per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="394bc-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="394bc-397">Come configurare il supporto di una rete virtuale per una Cache Redis di Azure Premium</span><span class="sxs-lookup"><span data-stu-id="394bc-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="394bc-398">Per altri dettagli su dimensioni, velocità effettiva e larghezza di banda con le cache Premium, vedere [Domande frequenti su Cache Redis di Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) .</span><span class="sxs-lookup"><span data-stu-id="394bc-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

