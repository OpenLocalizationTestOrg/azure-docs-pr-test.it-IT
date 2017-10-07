---
title: aaaConnect Excel tooSQL Database | Documenti Microsoft
description: Informazioni su come Microsoft Excel di tooconnect tooAzure SQL database nel cloud hello. Importare i dati in Excel per creare report ed esplorare i dati.
services: sql-database
keywords: connettere excel toosql, importare dati tooexcel
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
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="126fa-105">La connessione a database SQL di Azure tooan di Excel e creare un report</span><span class="sxs-lookup"><span data-stu-id="126fa-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="126fa-106">La connessione a Excel tooa SQL database nel cloud hello e importare i dati e creare tabelle e grafici in base ai valori nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="126fa-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="126fa-107">In questa esercitazione che si imposterà connessione hello tra Excel e una tabella di database, salvare il file hello che archivia le informazioni di connessione dati e hello per Excel e quindi creare un grafico pivot da hello i valori del database.</span><span class="sxs-lookup"><span data-stu-id="126fa-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="126fa-108">Per iniziare, è necessario un database SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="126fa-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="126fa-109">Se non si dispone di uno, vedere [creare il primo database SQL](sql-database-get-started-portal.md) tooget un database con dati di esempio attivo e in esecuzione in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="126fa-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="126fa-110">Questo articolo descrive come importare i dati di esempio in Excel, ma è anche possibile seguire la procedura con dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="126fa-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="126fa-111">Sarà necessaria anche una copia di Excel.</span><span class="sxs-lookup"><span data-stu-id="126fa-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="126fa-112">In questa esercitazione viene usato [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="126fa-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="126fa-113">La connessione a database SQL tooa di Excel e creare un file odc</span><span class="sxs-lookup"><span data-stu-id="126fa-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="126fa-114">tooconnect Excel tooSQL aprire Excel e quindi creare una nuova cartella di lavoro o aprire una cartella di lavoro di Excel esistente.</span><span class="sxs-lookup"><span data-stu-id="126fa-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="126fa-115">Nella barra dei menu hello nella parte superiore di hello di hello pagina fare clic su **dati**, fare clic su **da altre origini**, quindi fare clic su **da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="126fa-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Seleziona l'origine dati: la connessione a database tooSQL Excel.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="126fa-117">verrà visualizzata la finestra di Hello connessione guidata dati.</span><span class="sxs-lookup"><span data-stu-id="126fa-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="126fa-118">In hello **connettersi tooDatabase Server** hello tipo Database SQL nella finestra di dialogo **nome Server** tooconnect tooin hello modulo <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="126fa-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="126fa-119">Ad esempio, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="126fa-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="126fa-120">In **credenziali di accesso**, fare clic su **hello utilizzare seguito nome utente e Password**, hello tipo **nome utente** e **Password** è impostato su Hello server di Database SQL quando viene creato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="126fa-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Digitare le credenziali di nome e l'account di accesso server hello](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="126fa-122">A seconda dell'ambiente di rete, potrebbe non essere in grado di tooconnect o connessione hello vadano perduti se il server di Database SQL di hello non consentire il traffico verso l'indirizzo IP client.</span><span class="sxs-lookup"><span data-stu-id="126fa-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="126fa-123">Passare toohello [portale di Azure](https://portal.azure.com/), fare clic su SQL Server, fare clic sul server, scegliere le impostazioni di firewall e aggiungere l'indirizzo IP client.</span><span class="sxs-lookup"><span data-stu-id="126fa-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="126fa-124">Vedere [come impostazioni del firewall tooconfigure](sql-database-configure-firewall-settings.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="126fa-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="126fa-125">In hello **seleziona Database e tabella** finestra di dialogo, database selezionare hello desidera toowork con elenco hello e quindi fare clic su tabelle hello o viste che si desidera toowork con (è stato scelto **vGetAllCategories**), quindi Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="126fa-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selezionare un database e una tabella.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="126fa-127">Hello **Salva File di connessione dati e di fine** viene visualizzata la finestra di dialogo, in cui immettere informazioni la file hello Office database connection (*. odc) utilizzato da Excel.</span><span class="sxs-lookup"><span data-stu-id="126fa-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="126fa-128">È possibile lasciare le impostazioni predefinite hello o personalizzare le selezioni.</span><span class="sxs-lookup"><span data-stu-id="126fa-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="126fa-129">È possibile lasciare le impostazioni predefinite hello, ma hello nota **nome File** in particolare.</span><span class="sxs-lookup"><span data-stu-id="126fa-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="126fa-130">A **descrizione**, **nome descrittivo**, e **parole** consentono e ricordare di altri utenti si connette tooand trovare la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="126fa-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="126fa-131">Fare clic su **toouse prova sempre dati del file toorefresh** se si desiderano che le informazioni di connessione archiviate in file con estensione odc hello in modo che può aggiornare quando connette tooit e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="126fa-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Salvataggio di un file ODC](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="126fa-133">Hello **importare dati** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="126fa-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="126fa-134">Importare dati hello in Excel e creare un grafico pivot</span><span class="sxs-lookup"><span data-stu-id="126fa-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="126fa-135">Hai stabilita connessione hello e file hello creato con le informazioni di connessione e i dati, si sta leggendo dati hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="126fa-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="126fa-136">In hello **l'importazione dei dati** finestra di dialogo, fare clic su hello desiderato per presentare i dati nel foglio di lavoro hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="126fa-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="126fa-137">In questo caso è stato scelto **Grafico pivot**.</span><span class="sxs-lookup"><span data-stu-id="126fa-137">We chose **PivotChart**.</span></span> <span data-ttu-id="126fa-138">È anche possibile scegliere toocreate un **nuovo foglio di lavoro** o troppo**aggiungere questo modello di dati di tooa dati**.</span><span class="sxs-lookup"><span data-stu-id="126fa-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="126fa-139">Per altre informazioni sui modelli di dati, vedere [Creare un modello di dati in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="126fa-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="126fa-140">Fare clic su **proprietà** tooexplore informazioni file odc hello è stato creato in hello precedente passaggio e toochoose opzioni per l'aggiornamento dati hello.</span><span class="sxs-lookup"><span data-stu-id="126fa-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Scelta di hello formato per i dati in Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="126fa-142">foglio di lavoro Hello dispone ora di un grafico e una tabella pivot vuota.</span><span class="sxs-lookup"><span data-stu-id="126fa-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="126fa-143">In **PivotTable Fields**, selezionare tutti hello caselle di controllo per hello campi che si desidera tooview.</span><span class="sxs-lookup"><span data-stu-id="126fa-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Configurare un report di database.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="126fa-145">Se si desidera tooconnect altri database toohello cartelle di lavoro e fogli di lavoro di Excel, fare clic su **dati**, fare clic su **connessioni**, fare clic su **Aggiungi**, scegliere connessione hello è stato creato elenco di hello e quindi fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="126fa-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="126fa-146">![Aprire una connessione da un'altra cartella di lavoro](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="126fa-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="126fa-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="126fa-147">Next steps</span></span>
* <span data-ttu-id="126fa-148">Informazioni su come troppo[connettersi tooSQL Database con SQL Server Management Studio](sql-database-connect-query-ssms.md) avanzati di analisi e l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="126fa-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="126fa-149">Informazioni sui vantaggi hello [pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="126fa-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="126fa-150">Informazioni su come troppo[creare un'applicazione web che si connette tooSQL Database back-end hello](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="126fa-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

