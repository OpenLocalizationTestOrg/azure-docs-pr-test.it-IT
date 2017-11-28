---
title: i log di sito Web aaaAnalyze usando Azure Data Lake Analitica | Documenti Microsoft
description: 'Informazioni su come sito Web tooanalyze registra utilizzando Data Lake Analitica. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="d56bc-103">Analizzare i log dei siti Web con Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d56bc-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="d56bc-104">Informazioni su come i log di sito Web di tooanalyze tramite Data Lake Analitica, specialmente su come individuare quali riferimenti eseguito errori quando ha tentato di sito Web di hello toovisit.</span><span class="sxs-lookup"><span data-stu-id="d56bc-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d56bc-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d56bc-105">Prerequisites</span></span>
* <span data-ttu-id="d56bc-106">**Visual Studio 2015 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="d56bc-107">**[Data Lake Tools per Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="d56bc-108">Una volta Data Lake Tools per Visual Studio è installato, verrà visualizzato un **Data Lake** elemento hello **strumenti** menu in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d56bc-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="d56bc-110">**Conoscenza di base del Data Lake Analitica e hello Data Lake Tools per Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="d56bc-111">tooget introduzione, vedere:</span><span class="sxs-lookup"><span data-stu-id="d56bc-111">tooget started, see:</span></span>

  * <span data-ttu-id="d56bc-112">[Sviluppare script U-SQL con Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d56bc-113">**Account Analisi Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="d56bc-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="d56bc-114">Vedere la sezione relativa alla [creazione di un account di Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="d56bc-115">**Caricamento account Data Lake Analitica toohello di hello esempio dati.**</span><span class="sxs-lookup"><span data-stu-id="d56bc-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="d56bc-116">Vedere [file di dati di esempio toocopy](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="d56bc-117">un processo di Data Lake Analitica toorun, sarà necessario alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="d56bc-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="d56bc-118">Anche se hello Data Lake Tools supporta il caricamento di dati, si utilizzerà hello tooupload portale hello esempio dati toomake questa esercitazione toofollow più semplice.</span><span class="sxs-lookup"><span data-stu-id="d56bc-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="d56bc-119">Connettersi tooAzure</span><span class="sxs-lookup"><span data-stu-id="d56bc-119">Connect tooAzure</span></span>
<span data-ttu-id="d56bc-120">Prima di poter compilare e testare qualsiasi script U-SQL, è necessario innanzitutto connettersi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d56bc-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="d56bc-121">**tooconnect tooData Lake Analitica**</span><span class="sxs-lookup"><span data-stu-id="d56bc-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="d56bc-122">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d56bc-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="d56bc-123">Fare clic su **Data Lake > Opzioni e impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="d56bc-124">Fare clic su **Accedi**, o **Cambia utente** se un utente ha effettuato l'accesso e seguire le istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="d56bc-125">Fare clic su **OK** finestra Opzioni e impostazioni di hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="d56bc-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="d56bc-126">**toobrowse agli account Data Lake Analitica**</span><span class="sxs-lookup"><span data-stu-id="d56bc-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="d56bc-127">In Visual Studio aprire **Esplora server** premendo i tasti **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="d56bc-128">Da **Esplora server** espandere **Azure** e quindi **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="d56bc-129">Verrà visualizzato l'elenco degli account di Analisi Data Lake personali, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="d56bc-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="d56bc-130">È possibile creare gli account Data Lake Analitica da studio hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="d56bc-131">toocreate un account, vedere [Guida introduttiva di Azure Data Lake Analitica tramite il portale di Azure](data-lake-analytics-get-started-portal.md) o [Guida introduttiva di Azure Data Lake Analitica con Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="d56bc-132">Sviluppare un'applicazione U-SQL</span><span class="sxs-lookup"><span data-stu-id="d56bc-132">Develop U-SQL application</span></span>
<span data-ttu-id="d56bc-133">Un'applicazione U-SQL è principalmente uno script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d56bc-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="d56bc-134">toolearn ulteriori informazioni su U-SQL, vedere [introduzione U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="d56bc-135">È possibile aggiungere l'applicazione di toohello aggiunta agli operatori definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d56bc-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="d56bc-136">Per altre informazioni, vedere [Sviluppare operatori U-SQL definiti dall'utente per i processi di Analisi Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="d56bc-137">**toocreate e inviare un processo di Data Lake Analitica**</span><span class="sxs-lookup"><span data-stu-id="d56bc-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="d56bc-138">Fare clic su hello **File > Nuovo > progetto**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="d56bc-139">Selezionare il tipo di progetto U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-139">Select hello U-SQL Project type.</span></span>

    ![nuovo progetto U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="d56bc-141">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-141">Click **OK**.</span></span> <span data-ttu-id="d56bc-142">Visual Studio crea una soluzione con un file Script.usql.</span><span class="sxs-lookup"><span data-stu-id="d56bc-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="d56bc-143">Immettere lo script seguente nel file Script.usql hello hello:</span><span class="sxs-lookup"><span data-stu-id="d56bc-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="d56bc-144">hello toounderstand U-SQL, vedere [Introduzione a Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="d56bc-145">Aggiungere un nuovo progetto di tooyour script U-SQL e immettere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="d56bc-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="d56bc-146">Passare script U-SQL prima toohello indietro e Avanti toohello **Invia** pulsante, specificare l'account Analitica.</span><span class="sxs-lookup"><span data-stu-id="d56bc-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="d56bc-147">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script).</span><span class="sxs-lookup"><span data-stu-id="d56bc-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="d56bc-148">Verificare i risultati di hello nel riquadro di Output di hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="d56bc-149">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script).</span><span class="sxs-lookup"><span data-stu-id="d56bc-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="d56bc-150">Verificare hello **Account Analitica** è hello uno in cui si desidera toorun hello processo e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="d56bc-151">Risultati di invio e il collegamento di processo sono disponibili in hello Data Lake Tools per Visual Studio risultati quando viene completato l'invio di hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="d56bc-152">Attendere che il processo di hello viene completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d56bc-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="d56bc-153">Se ha esito negativo processo hello, molto probabilmente manca il file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d56bc-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="d56bc-154">Verificare hello nella sezione dei prerequisiti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d56bc-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="d56bc-155">Per altre informazioni sulla risoluzione dei problemi, vedere [Monitoraggio e risoluzione dei problemi dei processi di Analisi Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d56bc-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="d56bc-156">Al termine dell'esecuzione processo hello, vedrai hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="d56bc-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![Analisi Data Lake analizzare i log dei siti Web log dei siti Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="d56bc-158">Ripetere i passaggi da 7 a 10 per **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="d56bc-159">**output del processo hello toosee**</span><span class="sxs-lookup"><span data-stu-id="d56bc-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="d56bc-160">Da **Esplora Server**, espandere **Azure**, espandere **Data Lake Analitica**, espandere l'account Data Lake Analitica **gliaccountdiarchiviazione**, fare doppio clic su account di archiviazione dei dati Lake hello predefinito e quindi fare clic su **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="d56bc-161">Fare doppio clic su **esempi** tooopen hello cartella e quindi fare doppio clic su **output**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="d56bc-162">Fare doppio clic su **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="d56bc-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="d56bc-163">È possibile anche fare doppio clic sul file di output di hello in visualizzazione grafico hello del processo di hello in ordine toonavigate direttamente toohello output.</span><span class="sxs-lookup"><span data-stu-id="d56bc-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="d56bc-164">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d56bc-164">See also</span></span>
<span data-ttu-id="d56bc-165">tooget introduttiva Data Lake Analitica usando strumenti diversi, vedere:</span><span class="sxs-lookup"><span data-stu-id="d56bc-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="d56bc-166">Introduzione a Analisi Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d56bc-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d56bc-167">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d56bc-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="d56bc-168">Introduzione ad Analisi Data Lake mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d56bc-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
