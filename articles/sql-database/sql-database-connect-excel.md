---
title: Connettere Excel al database SQL | Documentazione Microsoft
description: Informazioni su come connettere Microsoft Excel al database SQL di Azure nel cloud. Importare i dati in Excel per creare report ed esplorare i dati.
services: sql-database
keywords: connettere Excel a SQL, importare i dati in Excel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="0a6f7-105">Connettere Excel a un database SQL di Azure e creare un report</span><span class="sxs-lookup"><span data-stu-id="0a6f7-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="0a6f7-106">Connettere Excel a un database SQL nel cloud, importare dati e creare tabelle e grafici in base ai valori nel database.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="0a6f7-107">In questa esercitazione sarà necessario configurare la connessione tra Excel e una tabella di database, salvare il file che archivia i dati e le informazioni di connessione per Excel e quindi creare un grafico pivot dai valori del database.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="0a6f7-108">Per iniziare, è necessario un database SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="0a6f7-109">Se non ne è già stato creato uno, vedere [Creare il primo database SQL di Azure](sql-database-get-started-portal.md) per ottenere un database con dati di esempio operativo in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="0a6f7-110">Questo articolo descrive come importare i dati di esempio in Excel, ma è anche possibile seguire la procedura con dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="0a6f7-111">Sarà necessaria anche una copia di Excel.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="0a6f7-112">In questa esercitazione viene usato [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="0a6f7-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="0a6f7-113">Connettere Excel a un database SQL e creare un file con estensione odc</span><span class="sxs-lookup"><span data-stu-id="0a6f7-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="0a6f7-114">Per connettere Excel a un database SQL, aprire Excel e quindi creare una nuova cartella di lavoro o aprirne una esistente.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="0a6f7-115">Nella barra dei menu nella parte superiore della pagina fare clic su **Dati**, quindi su **Da altre origini** e infine su **Da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selezione dell'origine dati: connettere Excel al database SQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="0a6f7-117">Si apre la Connessione guidata dati.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="0a6f7-118">Nella finestra di dialogo **Connessione al server di database** digitare il **Nome del server** per il database SQL a cui si vuole stabilire la connessione nel formato <*nomeserver*>**.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="0a6f7-119">Ad esempio, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="0a6f7-120">In **Credenziali di accesso** fare clic su **Usa nome utente e password seguenti**, digitare il **Nome utente** e la **Password** configurati per il server di database SQL quando è stato creato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Digitare il nome del server e le credenziali di accesso](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="0a6f7-122">A seconda dell'ambiente di rete, è possibile che non si riesca a connettersi o che si perda la connessione se il server di database SQL non consente il traffico dall'indirizzo IP client dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="0a6f7-123">Accedere al [portale di Azure](https://portal.azure.com/), fare clic su SQL Server, fare clic sul server, selezionare il firewall nelle impostazioni e aggiungere l'indirizzo IP del client.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="0a6f7-124">Per altre informazioni, vedere [Procedura: Configurare le impostazioni del firewall nel database SQL](sql-database-configure-firewall-settings.md) .</span><span class="sxs-lookup"><span data-stu-id="0a6f7-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="0a6f7-125">Nella finestra di dialogo **Seleziona database e tabella**, selezionare dall'elenco il database si vuole utilizzare e quindi fare clic sulle tabelle o sulle viste da utilizzare, in questo caso è stato scelto **vGetAllCategories**, e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selezionare un database e una tabella.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="0a6f7-127">Verrà visualizzata la finestra di dialogo **Salva file di connessione dati e chiudi** dove è si forniscono le informazioni sul file Office database connection (*.odc) usato da Excel.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="0a6f7-128">È possibile lasciare le impostazioni predefinite o personalizzare le selezioni.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="0a6f7-129">Si possono mantenere le impostazioni predefinite, ma notare in particolare il **Nome file** .</span><span class="sxs-lookup"><span data-stu-id="0a6f7-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="0a6f7-130">Le voci **Descrizione**, **Nome descrittivo** e **Parole chiave di ricerca** consentono a tutti gli utenti di ricordare e trovare la connessione.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="0a6f7-131">Fare clic su **Prova sempre a utilizzare questo file per l'aggiornamento dei dati** se si vogliono archiviare le informazioni sulla connessione nel file ODC, in modo che sia aggiornato quando viene usato durante la connessione, e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Salvataggio di un file ODC](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="0a6f7-133">Verrà visualizzata la finestra di dialogo **Importa dati** .</span><span class="sxs-lookup"><span data-stu-id="0a6f7-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="0a6f7-134">Importare i dati in Excel e creare un grafico pivot</span><span class="sxs-lookup"><span data-stu-id="0a6f7-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="0a6f7-135">Dopo aver stabilito la connessione e creato il file con dati e informazioni sulla connessione, è possibile prepararsi a importare i dati.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="0a6f7-136">Nella finestra di dialogo **Importa dati** fare clic sull'opzione da usare per presentare i dati nel foglio di lavoro e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="0a6f7-137">In questo caso è stato scelto **Grafico pivot**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-137">We chose **PivotChart**.</span></span> <span data-ttu-id="0a6f7-138">È anche possibile scegliere di creare un **Nuovo foglio di lavoro** o **Aggiungi questi dati al modello di dati**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="0a6f7-139">Per altre informazioni sui modelli di dati, vedere [Creare un modello di dati in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="0a6f7-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="0a6f7-140">Fare clic su **Proprietà** per esaminare le informazioni sul file ODC creato nel passaggio precedente e scegliere le opzioni per l'aggiornamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Scelta del formato per i dati in Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="0a6f7-142">Il foglio di lavoro include ora una tabella e un grafico pivot vuoti.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="0a6f7-143">In **Campi tabella pivot**, selezionare tutte le caselle di controllo per i campi da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Configurare un report di database.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="0a6f7-145">Per connettere altre cartelle di lavoro e fogli di lavoro di Excel al database, fare clic su **Dati**, fare clic su **Connessioni**, su **Aggiungi**, scegliere la connessione creata dall'elenco e quindi fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="0a6f7-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="0a6f7-146">![Aprire una connessione da un'altra cartella di lavoro](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="0a6f7-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0a6f7-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a6f7-147">Next steps</span></span>
* <span data-ttu-id="0a6f7-148">Per query e analisi avanzate, vedere [Connettersi al database SQL con SQL Server Management Studio](sql-database-connect-query-ssms.md) .</span><span class="sxs-lookup"><span data-stu-id="0a6f7-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="0a6f7-149">Informazioni sui vantaggi dei [pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="0a6f7-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="0a6f7-150">Informazioni su come [creare un'app Web che si connette al database SQL nel back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0a6f7-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

