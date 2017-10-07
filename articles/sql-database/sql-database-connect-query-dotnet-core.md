---
title: aaaUse .NET Core tooquery Database SQL di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come toouse .NET Core toocreate un programma che si connette tooan Database SQL di Azure ed eseguire una query utilizzando istruzioni Transact-SQL.
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
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="89ae0-103">Utilizzare .NET Core (c#) tooquery un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="89ae0-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="89ae0-104">Questa esercitazione introduttiva illustra come toouse [.NET Core](https://www.microsoft.com/net/) in Linux/Windows/macOS toocreate c# programma tooconnect tooan Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="89ae0-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89ae0-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="89ae0-105">Prerequisites</span></span>

<span data-ttu-id="89ae0-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="89ae0-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="89ae0-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="89ae0-107">An Azure SQL database.</span></span> <span data-ttu-id="89ae0-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="89ae0-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="89ae0-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="89ae0-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="89ae0-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="89ae0-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="89ae0-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="89ae0-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="89ae0-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="89ae0-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="89ae0-113">Avere installato [.NET Core per il sistema operativo](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="89ae0-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="89ae0-114">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="89ae0-114">SQL server connection information</span></span>

<span data-ttu-id="89ae0-115">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="89ae0-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="89ae0-116">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="89ae0-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="89ae0-117">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="89ae0-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="89ae0-118">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="89ae0-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="89ae0-119">In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="89ae0-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="89ae0-120">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="89ae0-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="89ae0-122">Se si dimenticano le informazioni di accesso del server Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server.</span><span class="sxs-lookup"><span data-stu-id="89ae0-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="89ae0-123">Se necessario, è possibile reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="89ae0-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="89ae0-124">Fare clic su **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="89ae0-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="89ae0-125">Hello revisione completa **ADO.NET** stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="89ae0-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Stringa di connessione ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="89ae0-127">Sul posto per l'indirizzo IP pubblico hello del computer hello in cui si esegue questa esercitazione, è necessario disporre una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="89ae0-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="89ae0-128">Se in un computer diverso o di un diverso indirizzo IP pubblico, creare un [regola firewall di livello server utilizzando il portale di Azure di hello](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="89ae0-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="89ae0-129">Creare un nuovo progetto .NET</span><span class="sxs-lookup"><span data-stu-id="89ae0-129">Create a new .NET project</span></span>

1. <span data-ttu-id="89ae0-130">Aprire un prompt dei comandi e creare una cartella denominata *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="89ae0-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="89ae0-131">Esplorazione delle cartelle toohello è creare ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="89ae0-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="89ae0-132">Aprire ***sqltest.csproj*** con un editor di testo e aggiungere SqlClient come dipendenza utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="89ae0-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="89ae0-133">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="89ae0-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="89ae0-134">Nell'ambiente di sviluppo o nell'editor di testo preferito aprire **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="89ae0-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="89ae0-135">Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="89ae0-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="89ae0-136">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="89ae0-136">Run hello code</span></span>

1. <span data-ttu-id="89ae0-137">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="89ae0-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="89ae0-138">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="89ae0-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="89ae0-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89ae0-139">Next steps</span></span>

- <span data-ttu-id="89ae0-140">[Introduzione a .NET Core in Windows o Linux/macOS tramite riga di comando hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="89ae0-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="89ae0-141">Informazioni su come troppo[connettersi ed eseguire query su un database SQL di Azure mediante hello .NET framework e Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="89ae0-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="89ae0-142">Informazioni su come troppo[progettazione di un database SQL di Azure utilizzando SSMS](sql-database-design-first-database.md) o [progettazione di un database SQL di Azure usando .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="89ae0-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="89ae0-143">Per altre informazioni su .NET, vedere la [documentazione di .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="89ae0-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
