---
title: Usare .NET Core per eseguire query sul database SQL di Azure | Microsoft Docs
description: Questo argomento illustra come usare .NET Core per creare un programma che si connette a un database SQL di Azure ed esegue query usando istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 046322624d3b89bb983acee863534256fee94b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-core-c-to-query-an-azure-sql-database"></a><span data-ttu-id="74215-103">Usare .NET Core (C#) per eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="74215-103">Use .NET Core (C#) to query an Azure SQL database</span></span>

<span data-ttu-id="74215-104">Questa esercitazione introduttiva illustra come usare [.NET Core](https://www.microsoft.com/net/) in Windows/Linux/macOS per creare un programma C# per connettersi a un database SQL di Azure e usare istruzioni Transact-SQL per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="74215-104">This quick start tutorial demonstrates how to use [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS to create a C# program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74215-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="74215-105">Prerequisites</span></span>

<span data-ttu-id="74215-106">Per completare questa esercitazione introduttiva, accertarsi di avere:</span><span class="sxs-lookup"><span data-stu-id="74215-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="74215-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="74215-107">An Azure SQL database.</span></span> <span data-ttu-id="74215-108">Questa guida introduttiva usa le risorse create in una delle guide introduttive seguenti:</span><span class="sxs-lookup"><span data-stu-id="74215-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="74215-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="74215-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="74215-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="74215-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="74215-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="74215-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="74215-112">Una [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico del computer usato per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="74215-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="74215-113">Avere installato [.NET Core per il sistema operativo](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="74215-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="74215-114">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="74215-114">SQL server connection information</span></span>

<span data-ttu-id="74215-115">Ottenere le informazioni di connessione necessarie per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="74215-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="74215-116">Nelle procedure successive saranno necessari il nome completo del server, il nome del database e le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="74215-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="74215-117">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74215-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="74215-118">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="74215-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="74215-119">Nella pagina **Panoramica** per il database, verificare il nome completo del server, come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="74215-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="74215-120">È possibile passare il puntatore sul nome del server per visualizzare l'opzione **Fare clic per copiare**.</span><span class="sxs-lookup"><span data-stu-id="74215-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="74215-122">Se si dimenticano le informazioni di accesso per il server di database SQL di Azure, passare alla pagina del server di database SQL per visualizzare il nome dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="74215-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="74215-123">È possibile reimpostare la password, se necessario.</span><span class="sxs-lookup"><span data-stu-id="74215-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="74215-124">Fare clic su **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="74215-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="74215-125">Esaminare la stringa di connessione completa **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="74215-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Stringa di connessione ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="74215-127">È necessario avere una regola del firewall impostata per l'indirizzo IP pubblico del computer su cui si esegue questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="74215-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="74215-128">Se si usa un computer o un indirizzo IP pubblico diverso, creare una [regola del firewall a livello di server con il portale di Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="74215-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="74215-129">Creare un nuovo progetto .NET</span><span class="sxs-lookup"><span data-stu-id="74215-129">Create a new .NET project</span></span>

1. <span data-ttu-id="74215-130">Aprire un prompt dei comandi e creare una cartella denominata *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="74215-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="74215-131">Passare alla cartella creata ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="74215-131">Navigate to the folder you created and run the following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="74215-132">Aprire ***sqltest.csproj*** con l'editor di testo preferito e aggiungere System.Data.SqlClient come dipendenza usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="74215-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using the following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="74215-133">Inserire il codice per eseguire query sul database SQL</span><span class="sxs-lookup"><span data-stu-id="74215-133">Insert code to query SQL database</span></span>

1. <span data-ttu-id="74215-134">Nell'ambiente di sviluppo o nell'editor di testo preferito aprire **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="74215-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="74215-135">Sostituire il contenuto con il codice seguente e aggiungere i valori appropriati per il server, il database, l'utente e la password.</span><span class="sxs-lookup"><span data-stu-id="74215-135">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-the-code"></a><span data-ttu-id="74215-136">Eseguire il codice</span><span class="sxs-lookup"><span data-stu-id="74215-136">Run the code</span></span>

1. <span data-ttu-id="74215-137">Al prompt dei comandi eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="74215-137">At the command prompt, run the following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="74215-138">Verificare che vengano restituite le prime 20 righe e quindi chiudere la finestra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74215-138">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="74215-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74215-139">Next steps</span></span>

- <span data-ttu-id="74215-140">[Introduzione all'uso di .NET Core su Windows/Linux/macOS dalla riga di comando](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="74215-140">[Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="74215-141">Informazioni su come [connettersi ed eseguire query su un database SQL di Azure usando .NET Framework e Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="74215-141">Learn how to [connect and query an Azure SQL database using the .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="74215-142">Informazioni su come [progettare il primo database SQL di Azure con SSMS](sql-database-design-first-database.md) o su come [progettare il primo database SQL di Azure con .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="74215-142">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="74215-143">Per altre informazioni su .NET, vedere la [documentazione di .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="74215-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
