---
title: Caricare dati da SQL Server in Azure SQL Data Warehouse (SSIS) | Documentazione Microsoft
description: Illustra come creare un pacchetto di SQL Server Integration Services (SSIS) per spostare dati da una vasta gamma di origini dati in SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="b58b2-103">Caricare dati da SQL Server in Azure SQL Data Warehouse (SSIS)</span><span class="sxs-lookup"><span data-stu-id="b58b2-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b58b2-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="b58b2-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="b58b2-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="b58b2-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="b58b2-106">bcp</span><span class="sxs-lookup"><span data-stu-id="b58b2-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="b58b2-107">Creare un pacchetto di SQL Server Integration Services (SSIS) per caricare i dati da SQL Sever ad Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-108">È possibile, facoltativamente, ristrutturare, trasformare e pulire i dati man mano che passano attraverso il flusso di dati SSIS.</span><span class="sxs-lookup"><span data-stu-id="b58b2-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="b58b2-109">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b58b2-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="b58b2-110">Creare un nuovo progetto di Integration Services in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b58b2-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="b58b2-111">Connettersi a origini dati, inclusi SQL Server come origine e SQL Data Warehouse come destinazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="b58b2-112">Progettare un pacchetto SSIS che carica i dati dall'origine nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="b58b2-113">Eseguire il pacchetto SSIS per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="b58b2-114">Questa esercitazione usa SQL Server come origine dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="b58b2-115">SQL Server può essere eseguito in locale o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b58b2-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="b58b2-116">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="b58b2-116">Basic concepts</span></span>
<span data-ttu-id="b58b2-117">Il pacchetto è l'unità di lavoro in SSIS.</span><span class="sxs-lookup"><span data-stu-id="b58b2-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="b58b2-118">I pacchetti correlati sono raggruppati in progetti.</span><span class="sxs-lookup"><span data-stu-id="b58b2-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="b58b2-119">Progetti e pacchetti di progettazione vengono creati in Visual Studio con SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="b58b2-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="b58b2-120">Il processo di progettazione è di tipo visivo e consente di trascinare la selezione dei componenti dalla Casella degli strumenti all'area di progettazione, connettere tali componenti e impostare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="b58b2-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="b58b2-121">Dopo aver completato il pacchetto, è possibile distribuirlo facoltativamente in SQL Server per la gestione, la sicurezza e il monitoraggio completi.</span><span class="sxs-lookup"><span data-stu-id="b58b2-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="b58b2-122">Opzioni di caricamento dei dati con SSIS</span><span class="sxs-lookup"><span data-stu-id="b58b2-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="b58b2-123">SQL Server Integration Services (SSIS) è un set di strumenti flessibile che offre un'ampia gamma di opzioni per la connessione e il caricamento dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="b58b2-124">Usare una destinazione ADO.NET per connettersi a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-125">Questa esercitazione usa una destinazione ADO.NET perché include il minor numero di opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="b58b2-126">Usare una destinazione OLE DB per connettersi a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-127">Questa opzione può fornire prestazioni leggermente migliori rispetto alla destinazione ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="b58b2-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="b58b2-128">Usare l'attività di caricamento BLOB di Azure per inserire i dati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b58b2-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="b58b2-129">Usare quindi l'attività Esegui SQL di SSIS per avviare uno script di Polybase che carica i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-130">Delle tre opzioni elencate qui, questa è quella che offre le prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="b58b2-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="b58b2-131">Per ottenere l'attività di caricamento BLOB di Azure, scaricare [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="b58b2-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="b58b2-132">Per altre informazioni su Polybase, vedere la [Guida di PolyBase][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="b58b2-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b58b2-133">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b58b2-133">Before you start</span></span>
<span data-ttu-id="b58b2-134">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b58b2-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="b58b2-135">**SQL Server Integration Services (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="b58b2-136">SSIS è un componente di SQL Server e richiede una versione di valutazione o una versione con licenza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b58b2-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="b58b2-137">Per ottenere una versione di valutazione di SQL Server 2016 Preview, vedere la pagina delle [versioni di valutazione di SQL Server][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="b58b2-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="b58b2-138">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="b58b2-138">**Visual Studio**.</span></span> <span data-ttu-id="b58b2-139">Per ottenere la versione gratuita di Visual Studio Community Edition, vedere [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="b58b2-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="b58b2-140">**SQL Server Data Tools per Visual Studio (SSDT)**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="b58b2-141">Per ottenere SQL Server Data Tools per Visual Studio, vedere [Scaricare SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="b58b2-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="b58b2-142">**Dati di esempio**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-142">**Sample data**.</span></span> <span data-ttu-id="b58b2-143">Questa esercitazione usa dati di esempio, archiviati nel database di esempio AdventureWorks in SQL Server, come dati di origine da caricare in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-144">Per ottenere il database di esempio AdventureWorks, vedere la pagina dei [database di esempio AdventureWorks 2014][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="b58b2-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="b58b2-145">**Database di SQL Data Warehouse e relative autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="b58b2-146">Questa esercitazione si connette a un'istanza di SQL Data Warehouse e vi carica i dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="b58b2-147">È necessario avere le autorizzazioni per creare una tabella e caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="b58b2-148">**Regola del firewall**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-148">**A firewall rule**.</span></span> <span data-ttu-id="b58b2-149">Per poter caricare dati in SQL Data Warehouse, è necessario creare una regola del firewall in SQL Data Warehouse con l'indirizzo IP del computer locale.</span><span class="sxs-lookup"><span data-stu-id="b58b2-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="b58b2-150">Passaggio 1: Creare un nuovo progetto di Integration Services</span><span class="sxs-lookup"><span data-stu-id="b58b2-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="b58b2-151">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b58b2-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="b58b2-152">Scegliere **Nuovo | Progetto** dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="b58b2-153">Passare ai tipi di progetto **Installati | Modelli | Business Intelligence | Integration Services** .</span><span class="sxs-lookup"><span data-stu-id="b58b2-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="b58b2-154">Selezionare **Progetto di Integration Services**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="b58b2-155">Specificare i valori per **Nome** e **Percorso** e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="b58b2-156">Visual Studio viene aperto e crea un nuovo progetto di Integration Services (SSIS).</span><span class="sxs-lookup"><span data-stu-id="b58b2-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="b58b2-157">Visual Studio apre quindi la finestra di progettazione per il nuovo pacchetto SSIS singolo (package.dtsx) nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b58b2-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="b58b2-158">Vengono visualizzate le aree dello schermo seguenti:</span><span class="sxs-lookup"><span data-stu-id="b58b2-158">You see the following screen areas:</span></span>

* <span data-ttu-id="b58b2-159">A sinistra la **Casella degli strumenti** dei componenti SSIS.</span><span class="sxs-lookup"><span data-stu-id="b58b2-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="b58b2-160">Al centro l'area di progettazione con più schede.</span><span class="sxs-lookup"><span data-stu-id="b58b2-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="b58b2-161">In genere si usano almeno le schede **Flusso di controllo** e **Flusso di dati**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="b58b2-162">A destra i riquadri **Esplora soluzioni** e **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="b58b2-163">Passaggio 2: Creare il flusso di dati di base</span><span class="sxs-lookup"><span data-stu-id="b58b2-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="b58b2-164">Trascinare un'attività Flusso di dati dalla Casella degli strumenti al centro dell'area di progettazione, nella scheda **Flusso di controllo** .</span><span class="sxs-lookup"><span data-stu-id="b58b2-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="b58b2-165">Fare doppio clic sull'attività Flusso di dati per passare alla scheda Flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="b58b2-166">Dall'elenco Altre origini nella Casella degli strumenti trascinare un'origine ADO.NET nell'area di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="b58b2-167">Con l'adattatore di origine ancora selezionato modificare il nome in **Origine SQL Server** nel riquadro **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="b58b2-168">Dall'elenco Altre destinazioni nella Casella degli strumenti trascinare una destinazione ADO.NET nell'area di progettazione sotto l'origine ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="b58b2-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="b58b2-169">Con l'adattatore di destinazione ancora selezionato modificare il nome in **Destinazione SQL DW** nel riquadro **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="b58b2-170">Passaggio 3: Configurare l'adattatore di origine</span><span class="sxs-lookup"><span data-stu-id="b58b2-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="b58b2-171">Fare doppio clic sull'adattatore di origine per aprire la **Editor origine ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="b58b2-172">Nella scheda **Gestione connessione** di **Editor origine ADO.NET** fare clic sul pulsante **Nuovo** accanto all'elenco **Gestione connessione ADO.NET** per aprire la finestra di dialogo **Configura gestione connessione ADO.NET** e creare le impostazioni di connessione per il database SQL Server da cui questa esercitazione carica i dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="b58b2-173">Nella finestra di dialogo **Configura gestione connessione ADO.NET** fare clic sul pulsante **Nuovo** per aprire la finestra di dialogo **Gestione connessione** e creare una nuova connessione dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="b58b2-174">Nella finestra di dialogo **Gestione connessione** eseguire queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="b58b2-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="b58b2-175">Per **Provider**selezionare il provider di dati SqlClient.</span><span class="sxs-lookup"><span data-stu-id="b58b2-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="b58b2-176">Per **Nome server**immettere il nome di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b58b2-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="b58b2-177">Nella sezione **Accesso al server** selezionare o immettere le informazioni di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="b58b2-178">Nella sezione **Connessione al database** selezionare il database di esempio AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="b58b2-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="b58b2-179">Fare clic su **Test connessione**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="b58b2-180">Nella finestra di dialogo che segnala i risultati del test di connessione fare clic su **OK** per tornare alla finestra di dialogo **Gestione connessione**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="b58b2-181">Nella finestra di dialogo **Gestione connessione** fare clic su **OK** per tornare alla finestra di dialogo **Configura gestione connessione ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="b58b2-182">Nella finestra di dialogo **Configura gestione connessione ADO.NET** fare clic su **OK** per tornare a **Editor origine ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="b58b2-183">Nell'elenco **Nome della tabella o Nome della vista** in **Editor origine ADO.NET** selezionare la tabella **Sales.SalesOrderDetail**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="b58b2-184">Fare clic su **Anteprima** per visualizzare le prime 200 righe di dati nella tabella di origine nella finestra di dialogo **Anteprima risultati query**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="b58b2-185">Nella finestra di dialogo **Anteprima risultati query** fare clic su **Chiudi** per tornare a **Editor origine ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="b58b2-186">In **Editor origine ADO.NET** fare clic su **OK** per completare la configurazione dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="b58b2-187">Passaggio 4: Connettere l'adattatore di origine all'adattatore di destinazione</span><span class="sxs-lookup"><span data-stu-id="b58b2-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="b58b2-188">Selezionare l'adattatore di origine nell'area di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="b58b2-189">Selezionare la freccia blu che si estende dall'adattatore di origine e trascinarla nell'editor di destinazione finché non si ancora.</span><span class="sxs-lookup"><span data-stu-id="b58b2-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="b58b2-190">In un pacchetto SSIS tipico si usano molti altri componenti dalla Casella degli strumenti di SSIS tra l'origine e destinazione per ristrutturare, trasformare e pulire i dati man mano che passano attraverso il flusso di dati SSIS.</span><span class="sxs-lookup"><span data-stu-id="b58b2-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="b58b2-191">Per mantenere questo esempio il più semplice possibile, l'origine viene connessa direttamente alla destinazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="b58b2-192">Passaggio 5: Configurare l'adattatore di destinazione</span><span class="sxs-lookup"><span data-stu-id="b58b2-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="b58b2-193">Fare doppio clic sull'adattatore di destinazione per aprire **Editor destinazione ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="b58b2-194">Nella scheda **Gestione connessione** di **Editor destinazione ADO.NET** fare clic sul pulsante **Nuovo** accanto all'elenco **Gestione connessione** per aprire la finestra di dialogo **Configura gestione connessione ADO.NET** e creare le impostazioni di connessione per il database di Azure SQL Data Warehouse in cui questa esercitazione carica i dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="b58b2-195">Nella finestra di dialogo **Configura gestione connessione ADO.NET** fare clic sul pulsante **Nuovo** per aprire la finestra di dialogo **Gestione connessione** e creare una nuova connessione dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="b58b2-196">Nella finestra di dialogo **Gestione connessione** eseguire queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="b58b2-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="b58b2-197">Per **Provider**selezionare il provider di dati SqlClient.</span><span class="sxs-lookup"><span data-stu-id="b58b2-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="b58b2-198">Per **Nome server**immettere il nome di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="b58b2-199">Nella sezione **Accesso al server** selezionare **Usa autenticazione di SQL Server** e immettere le informazioni di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="b58b2-200">Nella sezione **Connessione al database** selezionare un database di SQL Data Warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="b58b2-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="b58b2-201">Fare clic su **Test connessione**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="b58b2-202">Nella finestra di dialogo che segnala i risultati del test di connessione fare clic su **OK** per tornare alla finestra di dialogo **Gestione connessione**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="b58b2-203">Nella finestra di dialogo **Gestione connessione** fare clic su **OK** per tornare alla finestra di dialogo **Configura gestione connessione ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="b58b2-204">Nella finestra di dialogo **Configura gestione connessione ADO.NET** fare clic su **OK** per tornare a **Editor destinazione ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="b58b2-205">In **Editor destinazione ADO.NET** fare clic su **Nuovo** accanto all'elenco **Usa una tabella o una vista** per aprire la finestra di dialogo **Crea tabella** per creare una nuova tabella di destinazione con un elenco di colonne corrispondente alla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="b58b2-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="b58b2-206">Nella finestra di dialogo **Crea tabella** eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="b58b2-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="b58b2-207">Modificare il nome della tabella di destinazione in **SalesOrderDetail**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="b58b2-208">Rimuovere la colonna **rowguid** .</span><span class="sxs-lookup"><span data-stu-id="b58b2-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="b58b2-209">Il tipo di dati **uniqueidentifier** non è supportato in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="b58b2-210">Modificare il tipo di dati della colonna **LineTotal** in **money**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="b58b2-211">Il tipo di dati **decima** l non è supportato in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="b58b2-212">Per informazioni sui tipi di dati supportati, vedere [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="b58b2-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="b58b2-213">Fare clic su **OK** per creare la tabella e tornare a **Editor destinazione ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="b58b2-214">In **Editor destinazione ADO.NET** selezionare la scheda **Mapping** per vedere in che modo le colonne nell'origine vengono mappate alle colonne nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="b58b2-215">Fare clic su **OK** per completare la configurazione dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="b58b2-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="b58b2-216">Passaggio 6: Eseguire il pacchetto per caricare i dati</span><span class="sxs-lookup"><span data-stu-id="b58b2-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="b58b2-217">Per eseguire il pacchetto, fare clic sul pulsante **Avvia** sulla barra degli strumenti o selezionare una delle opzioni **Esegui** nel menu **Debug**.</span><span class="sxs-lookup"><span data-stu-id="b58b2-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="b58b2-218">Quando inizia l'esecuzione del pacchetto, verranno visualizzate rotelline gialle che ruotano per indicare l'attività, nonché il numero di righe elaborate.</span><span class="sxs-lookup"><span data-stu-id="b58b2-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="b58b2-219">Al termine dell'esecuzione del pacchetto vengono visualizzati segni di spunta verde per indicare che l'operazione è riuscita, nonché il numero totale di righe di dati caricati dall'origine alla destinazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="b58b2-220">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b58b2-220">Congratulations!</span></span> <span data-ttu-id="b58b2-221">SQL Server Integration Services è stato usato correttamente per caricare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b58b2-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b58b2-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b58b2-222">Next steps</span></span>
* <span data-ttu-id="b58b2-223">Altre informazioni relative al flusso di dati SSIS.</span><span class="sxs-lookup"><span data-stu-id="b58b2-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="b58b2-224">Iniziare da qui: [Flusso di dati][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="b58b2-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="b58b2-225">Informazioni su come eseguire il debug e risolvere i problemi relativi ai pacchetti direttamente nell'ambiente di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="b58b2-226">Iniziare da qui: [Strumenti per la risoluzione dei problemi di sviluppo di pacchetti][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="b58b2-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="b58b2-227">Informazioni su come distribuire i progetti e i pacchetti SSIS nel server Integration Services o in un altro percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b58b2-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="b58b2-228">Iniziare da qui: [Distribuzione di progetti e pacchetti][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="b58b2-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
