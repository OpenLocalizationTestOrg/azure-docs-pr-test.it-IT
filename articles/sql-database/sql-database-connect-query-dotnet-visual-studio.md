---
title: aaaUse .NET e Visual Studio tooquery Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse Visual Studio toocreate un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="fe7c5-103">Utilizzare .NET (c#) con Visual Studio tooconnect ed eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="fe7c5-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="fe7c5-104">Questa esercitazione introduttiva illustra come hello toouse [.NET framework](https://www.microsoft.com/net/) toocreate c# programmare con il database SQL di Azure di Visual Studio tooconnect tooan e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe7c5-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe7c5-105">Prerequisites</span></span>

<span data-ttu-id="fe7c5-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="fe7c5-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="fe7c5-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-107">An Azure SQL database.</span></span> <span data-ttu-id="fe7c5-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="fe7c5-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="fe7c5-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="fe7c5-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="fe7c5-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="fe7c5-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="fe7c5-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe7c5-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="fe7c5-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="fe7c5-113">Un'installazione di [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="fe7c5-114">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="fe7c5-114">SQL server connection information</span></span>

<span data-ttu-id="fe7c5-115">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="fe7c5-116">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="fe7c5-117">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fe7c5-118">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="fe7c5-119">In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="fe7c5-120">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="fe7c5-122">Se si dimenticano le informazioni di accesso del server Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="fe7c5-123">Se necessario, è possibile reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="fe7c5-124">Fare clic su **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="fe7c5-125">Hello revisione completa **ADO.NET** stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Stringa di connessione ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="fe7c5-127">Sul posto per l'indirizzo IP pubblico hello del computer hello in cui si esegue questa esercitazione, è necessario disporre una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="fe7c5-128">Se in un computer diverso o di un diverso indirizzo IP pubblico, creare un [regola firewall di livello server utilizzando il portale di Azure di hello](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="fe7c5-129">Creare un nuovo progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe7c5-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="fe7c5-130">In Visual Studio scegliere **File**, **Nuovo**, **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="fe7c5-131">In hello **nuovo progetto** finestra di dialogo espandere **Visual c#**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="fe7c5-132">Selezionare **App Console** e immettere *sqltest* hello nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="fe7c5-133">Fare clic su **OK** toocreate e hello Apri nuovo progetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe7c5-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="fe7c5-134">In Esplora soluzioni fare clic con il pulsante destro del mouse su **sqltest** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="fe7c5-135">In hello **Sfoglia**, cercare ```System.Data.SqlClient``` e, se trovato, selezionarla.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="fe7c5-136">In hello **SqlClient** pagina, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="fe7c5-137">Al termine dell'installazione di hello, rivedere le modifiche di hello e quindi fare clic su **OK** tooclose hello **anteprima** finestra.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="fe7c5-138">Se viene visualizzata una finestra **Accettazione della licenza** fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="fe7c5-139">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="fe7c5-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="fe7c5-140">Opzione troppo (o aprire se necessario) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="fe7c5-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="fe7c5-141">Sostituire il contenuto di hello di **Program.cs** con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="fe7c5-142">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="fe7c5-142">Run hello code</span></span>

1. <span data-ttu-id="fe7c5-143">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="fe7c5-144">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe7c5-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe7c5-145">Next steps</span></span>

- <span data-ttu-id="fe7c5-146">Informazioni su come troppo[connettersi ed eseguire query su un database SQL di Azure mediante .NET core](sql-database-connect-query-dotnet-core.md) su Linux/Windows/macOS.</span><span class="sxs-lookup"><span data-stu-id="fe7c5-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="fe7c5-147">Informazioni su [Introduzione a .NET Core in Windows o Linux/macOS tramite riga di comando hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="fe7c5-148">Informazioni su come troppo[progettazione di un database SQL di Azure utilizzando SSMS](sql-database-design-first-database.md) o [progettazione di un database SQL di Azure usando .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="fe7c5-149">Per altre informazioni su .NET, vedere la [documentazione di .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="fe7c5-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
