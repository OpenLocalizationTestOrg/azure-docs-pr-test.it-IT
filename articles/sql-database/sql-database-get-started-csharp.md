---
title: 'C#: introduzione al database SQL di Azure | Documentazione Microsoft'
description: Provare a Database SQL per lo sviluppo di applicazioni SQL e c# e creare un Database SQL di Azure con c# utilizzando hello SQL Database di libreria per .NET.
keywords: provare sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a><span data-ttu-id="500db-104">Usare c# toocreate un database SQL con hello SQL Database di libreria per .NET</span><span class="sxs-lookup"><span data-stu-id="500db-104">Use C# toocreate a SQL database with hello SQL Database Library for .NET</span></span>

<span data-ttu-id="500db-105">Informazioni su come toocreate toouse c# SQL Azure database con hello [libreria gestione SQL di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="500db-105">Learn how toouse C# toocreate an Azure SQL database with hello [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="500db-106">In questo articolo viene descritto come toocreate un singolo database di SQL e c#.</span><span class="sxs-lookup"><span data-stu-id="500db-106">This article describes how toocreate a single database with SQL and C#.</span></span> <span data-ttu-id="500db-107">pool elastico toocreate, vedere l'articolo [creare un pool elastico](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="500db-107">toocreate elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="500db-108">Hello libreria di gestione Database SQL Azure per .NET fornisce un [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-basato su API che esegue il wrapping hello [basate su Gestione risorse di API REST di Database SQL](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="500db-108">hello Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps hello [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="500db-109">Numerose nuove funzionalità di Database SQL sono supportate solo quando si utilizza hello [il modello di distribuzione Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), pertanto è consigliabile utilizzare sempre hello più recente **libreria di gestione Database SQL Azure per .NET ([documenti](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span><span class="sxs-lookup"><span data-stu-id="500db-109">Many new features of SQL Database are only supported when you are using hello [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use hello latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="500db-110">Hello precedente [librerie basate su modello di distribuzione classica](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) sono supportati per motivi di compatibilità, pertanto si consiglia di usare le librerie di gestione di risorse basato su più recenti hello.</span><span class="sxs-lookup"><span data-stu-id="500db-110">hello older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use hello newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="500db-111">passaggi di hello toocomplete in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="500db-111">toocomplete hello steps in this article, you need hello following:</span></span>

* <span data-ttu-id="500db-112">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="500db-112">An Azure subscription.</span></span> <span data-ttu-id="500db-113">Se è necessaria una sottoscrizione di Azure, è sufficiente fare clic su **ACCOUNT gratuito** nella parte superiore di hello di questa pagina e quindi tornare toofinish in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="500db-113">If you need an Azure subscription simply click **FREE ACCOUNT** at hello top of this page, and then come back toofinish this article.</span></span>
* <span data-ttu-id="500db-114">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="500db-114">Visual Studio.</span></span> <span data-ttu-id="500db-115">Per una copia gratuita di Visual Studio, vedere hello [download di Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) pagina.</span><span class="sxs-lookup"><span data-stu-id="500db-115">For a free copy of Visual Studio, see hello [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="500db-116">Questo articolo illustra la creazione di un nuovo database SQL vuoto.</span><span class="sxs-lookup"><span data-stu-id="500db-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="500db-117">Modificare hello *CreateOrUpdateDatabase(...)*  metodo in hello seguendo i database di esempio toocopy, ridimensionare i database, creare un database in un pool e così via.</span><span class="sxs-lookup"><span data-stu-id="500db-117">Modify hello *CreateOrUpdateDatabase(...)* method in hello following sample toocopy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a><span data-ttu-id="500db-118">Creare un'applicazione console e installare le librerie necessarie hello</span><span class="sxs-lookup"><span data-stu-id="500db-118">Create a console app and install hello required libraries</span></span>
1. <span data-ttu-id="500db-119">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="500db-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="500db-120">Fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="500db-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="500db-121">Creare un' **applicazione console** in C# e denominarla *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="500db-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="500db-122">le librerie di gestione di richieste toocreate un database SQL con c#, hello carico (usando hello [console di gestione pacchetti](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="500db-122">toocreate a SQL database with C#, load hello required management libraries (using hello [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="500db-123">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="500db-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="500db-124">Tipo `Install-Package Microsoft.Azure.Management.Sql -Pre` più recente hello tooinstall [libreria di gestione di Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="500db-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="500db-125">Tipo `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [libreria Gestione risorse di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="500db-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="500db-126">Tipo `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [libreria di autenticazione comune di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span><span class="sxs-lookup"><span data-stu-id="500db-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="500db-127">Hello esempi in questo articolo usano sincrona di ogni richiesta di API e il blocco fino al completamento della chiamata REST hello in hello servizio sottostante.</span><span class="sxs-lookup"><span data-stu-id="500db-127">hello examples in this article use a synchronous form of each API request and block until completion of hello REST call on hello underlying service.</span></span> <span data-ttu-id="500db-128">Sono disponibili metodi asincroni.</span><span class="sxs-lookup"><span data-stu-id="500db-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="500db-129">Creare un server di database SQL, una regola firewall e un database SQL: esempio di C#</span><span class="sxs-lookup"><span data-stu-id="500db-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="500db-130">Hello seguente esempio crea un gruppo di risorse, server, regola del firewall e un database SQL.</span><span class="sxs-lookup"><span data-stu-id="500db-130">hello following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="500db-131">Vedere, [creare risorse di un tooaccess dell'entità servizio](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variabili.</span><span class="sxs-lookup"><span data-stu-id="500db-131">See, [Create a service principal tooaccess resources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="500db-132">Sostituire il contenuto di hello di **Program.cs** con seguente hello e aggiornamento hello `{variables}` con i valori di app (non includono hello `{}`).</span><span class="sxs-lookup"><span data-stu-id="500db-132">Replace hello contents of **Program.cs** with hello following, and update hello `{variables}` with your app values (do not include hello `{}`).</span></span>

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a><span data-ttu-id="500db-133">Creare un tooaccess dell'entità servizio di risorse</span><span class="sxs-lookup"><span data-stu-id="500db-133">Create a service principal tooaccess resources</span></span>
<span data-ttu-id="500db-134">Hello script PowerShell seguente crea un'applicazione hello Active Directory (AD) e il servizio hello principale che è necessario tooauthenticate applicazione c#.</span><span class="sxs-lookup"><span data-stu-id="500db-134">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="500db-135">script Hello restituisce valori che è base per hello precedente c# di esempio.</span><span class="sxs-lookup"><span data-stu-id="500db-135">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="500db-136">Per informazioni dettagliate, vedere [toocreate usare Azure PowerShell un'entità servizio tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="500db-136">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="500db-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="500db-137">Next steps</span></span>
<span data-ttu-id="500db-138">Ora che si è provato a Database SQL e impostare un database con c#, si è pronti per hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="500db-138">Now that you've tried SQL Database and set up a database with C#, you're ready for hello following articles:</span></span>

* [<span data-ttu-id="500db-139">Connettersi tooSQL Database con SQL Server Management Studio ed eseguire una query T-SQL di esempio</span><span class="sxs-lookup"><span data-stu-id="500db-139">Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="500db-140">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="500db-140">Additional Resources</span></span>
* [<span data-ttu-id="500db-141">Database SQL</span><span class="sxs-lookup"><span data-stu-id="500db-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="500db-142">Classe di database</span><span class="sxs-lookup"><span data-stu-id="500db-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
