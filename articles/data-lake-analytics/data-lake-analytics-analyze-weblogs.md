---
title: Analizzare i log dei siti Web con Azure Data Lake Analytics | Documentazione Microsoft
description: 'Informazioni su come analizzare i log dei siti Web con Analisi Azure Data Lake. '
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="d0a66-103">Analizzare i log dei siti Web con Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d0a66-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="d0a66-104">Informazioni su come analizzare i log dei siti Web con Analisi Data Lake, in particolare come scoprire quali referrer hanno riscontrato errori durante la visita al il sito Web.</span><span class="sxs-lookup"><span data-stu-id="d0a66-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0a66-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0a66-105">Prerequisites</span></span>
* <span data-ttu-id="d0a66-106">**Visual Studio 2015 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="d0a66-107">**[Data Lake Tools per Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="d0a66-108">Dopo avere installato Strumenti Data Lake per Visual Studio, in Visual Studio verrà visualizzata una voce **Data Lake** nel menu **Strumenti**:</span><span class="sxs-lookup"><span data-stu-id="d0a66-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="d0a66-110">**Conoscenza di base di Analisi Data Lake e Data Lake Tools per Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="d0a66-111">Per iniziare, vedere:</span><span class="sxs-lookup"><span data-stu-id="d0a66-111">To get started, see:</span></span>

  * <span data-ttu-id="d0a66-112">[Sviluppare script U-SQL con Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d0a66-113">**Account Analisi Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="d0a66-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="d0a66-114">Vedere la sezione relativa alla [creazione di un account di Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="d0a66-115">**Caricare i dati di esempio nell'account Analisi Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="d0a66-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="d0a66-116">Vedere [Per copiare file di dati di esempio](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="d0a66-117">Per eseguire un processo di Analisi Data Lake, sanno necessari alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="d0a66-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="d0a66-118">Anche se Data Lake Tools supporta il caricamento di dati, si userà il portale per caricare i dati di esempio e seguire più facilmente questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d0a66-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="d0a66-119">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="d0a66-119">Connect to Azure</span></span>
<span data-ttu-id="d0a66-120">Prima di poter compilare e testare qualsiasi script U-SQL, è necessario connettersi ad Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a66-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="d0a66-121">**Per connettersi ad Analisi Data Lake**</span><span class="sxs-lookup"><span data-stu-id="d0a66-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="d0a66-122">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0a66-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="d0a66-123">Fare clic su **Data Lake > Opzioni e impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="d0a66-124">Fare clic su **Accedi** o **Cambia utente** se un altro utente ha già eseguito l'accesso e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="d0a66-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="d0a66-125">Fare clic su **OK** per chiudere la finestra di dialogo Opzioni e impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d0a66-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="d0a66-126">**Per accedere agli account Analisi Data Lake personali**</span><span class="sxs-lookup"><span data-stu-id="d0a66-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="d0a66-127">In Visual Studio aprire **Esplora server** premendo i tasti **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="d0a66-128">Da **Esplora server** espandere **Azure** e quindi **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="d0a66-129">Verrà visualizzato l'elenco degli account di Analisi Data Lake personali, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="d0a66-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="d0a66-130">Non è possibile creare account Analisi Data Lake da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0a66-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="d0a66-131">Per creare un account, vedere [Introduzione ad Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-get-started-portal.md) o [Introduzione ad Azure Data Lake Analytics con Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="d0a66-132">Sviluppare un'applicazione U-SQL</span><span class="sxs-lookup"><span data-stu-id="d0a66-132">Develop U-SQL application</span></span>
<span data-ttu-id="d0a66-133">Un'applicazione U-SQL è principalmente uno script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d0a66-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="d0a66-134">Per altre informazioni su U-SQL, vedere [Introduzione a U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="d0a66-135">È possibile aggiungere all'applicazione operatori addizione definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d0a66-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="d0a66-136">Per altre informazioni, vedere [Sviluppare operatori U-SQL definiti dall'utente per i processi di Analisi Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="d0a66-137">**Per creare e inviare un processo di Analisi Data Lake**</span><span class="sxs-lookup"><span data-stu-id="d0a66-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="d0a66-138">Fare clic su **File > Nuovo > Progetto**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="d0a66-139">Selezionare il tipo Progetto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d0a66-139">Select the U-SQL Project type.</span></span>

    ![nuovo progetto U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="d0a66-141">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-141">Click **OK**.</span></span> <span data-ttu-id="d0a66-142">Visual Studio crea una soluzione con un file Script.usql.</span><span class="sxs-lookup"><span data-stu-id="d0a66-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="d0a66-143">Immettere lo script seguente nel file Script.usql:</span><span class="sxs-lookup"><span data-stu-id="d0a66-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="d0a66-144">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL con Analisi Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="d0a66-145">Aggiungere al progetto un nuovo script U-SQL e immettere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d0a66-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="d0a66-146">Tornare al primo script U-SQL e accanto al pulsante **Invia** , specificare l'account di analisi.</span><span class="sxs-lookup"><span data-stu-id="d0a66-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="d0a66-147">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script).</span><span class="sxs-lookup"><span data-stu-id="d0a66-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="d0a66-148">Verificare il risultato nel riquadro di output.</span><span class="sxs-lookup"><span data-stu-id="d0a66-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="d0a66-149">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script).</span><span class="sxs-lookup"><span data-stu-id="d0a66-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="d0a66-150">Verificare che **Account Analisi** sia quello in cui si vuole eseguire il processo e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="d0a66-151">Al termine della procedura di invio, nella finestra dei risultati di Strumenti di Data Lake per Visual Studio saranno disponibili i risultati dell'operazione di invio e il collegamento al processo.</span><span class="sxs-lookup"><span data-stu-id="d0a66-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="d0a66-152">Attendere che il processo venga completato.</span><span class="sxs-lookup"><span data-stu-id="d0a66-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="d0a66-153">Se il processo non riesce, è molto probabile che manchi il file di origine.</span><span class="sxs-lookup"><span data-stu-id="d0a66-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="d0a66-154">Vedere la sezione Prerequisiti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d0a66-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="d0a66-155">Per altre informazioni sulla risoluzione dei problemi, vedere [Monitoraggio e risoluzione dei problemi dei processi di Analisi Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d0a66-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="d0a66-156">Una volta completato il processo, verrà visualizzata la schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="d0a66-156">When the job is completed, you shall see the following screen:</span></span>

    ![Analisi Data Lake analizzare i log dei siti Web log dei siti Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="d0a66-158">Ripetere i passaggi da 7 a 10 per **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="d0a66-159">**Per visualizzare l'output del processo**</span><span class="sxs-lookup"><span data-stu-id="d0a66-159">**To see the job output**</span></span>

1. <span data-ttu-id="d0a66-160">Da **Esplora server** espandere **Azure**, quindi **Data Lake Analytics**, l'account Data Lake Analytics e infine **Account di archiviazione**. Fare clic con il pulsante destro del mouse sull'account Data Lake Analytics predefinito e quindi scegliere **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="d0a66-161">Fare doppio clic su **Esempi** per aprire la cartella e quindi su **Output**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="d0a66-162">Fare doppio clic su **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="d0a66-163">È anche possibile fare doppio clic sul file di output nella visualizzazione grafico del processo per passare direttamente al file di output.</span><span class="sxs-lookup"><span data-stu-id="d0a66-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="d0a66-164">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d0a66-164">See also</span></span>
<span data-ttu-id="d0a66-165">Per iniziare a usare Analisi Data Lake usando vari tipi di strumenti, vedere:</span><span class="sxs-lookup"><span data-stu-id="d0a66-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="d0a66-166">Introduzione a Analisi Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0a66-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d0a66-167">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0a66-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="d0a66-168">Introduzione ad Analisi Data Lake mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d0a66-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
