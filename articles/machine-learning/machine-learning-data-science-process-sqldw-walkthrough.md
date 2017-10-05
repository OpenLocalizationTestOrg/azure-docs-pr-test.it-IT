---
title: 'Processo di analisi scientifica dei dati per i team in azione: uso di SQL Data Warehouse | Documentazione Microsoft'
description: Advanced Analytics Process and Technology in azione
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="e7ac4-103">Processo di analisi scientifica dei dati per i team in azione: uso di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="e7ac4-104">In questa esercitazione verranno esaminate la compilazione e la distribuzione di un modello di Machine Learning usando SQL Data Warehouse (SQL DW) per un set di dati disponibile pubblicamente, il set di dati [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="e7ac4-105">Il modello di classificazione binaria costruito stabilisce se sia stata lasciata o meno una mancia per una corsa. Vengono illustrati anche i modelli per la regressione e la classificazione multiclasse che consentono di stimare la distribuzione delle mance pagate.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="e7ac4-106">La procedura segue il flusso di lavoro del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="e7ac4-107">Viene illustrato come configurare un ambiente di scienza dei dati, come caricare i dati in SQL DW e come usare SQL DW o IPython Notebook per esplorare i dati e progettare le funzionalità da modellare.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="e7ac4-108">Viene quindi illustrato come compilare e distribuire un modello con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="e7ac4-109"><a name="dataset"></a>Set di dati NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="e7ac4-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="e7ac4-110">I dati di NYC Taxi Trip sono costituiti da circa 20 GB di file CSV compressi (circa 48 GB non compressi) e registrano oltre 173 milioni di corse singole nonché le tariffe pagate per ogni corsa.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="e7ac4-111">Il record di ogni corsa include le località e gli orari di partenza e di arrivo, il numero di patente anonimo (del tassista) e il numero di licenza (ID univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e7ac4-112">I dati sono relativi a tutte le corse per l'anno 2013 e vengono forniti nei due set di dati seguenti per ciascun mese:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="e7ac4-113">Il file **trip_data.csv** contiene i dettagli delle corse, ad esempio il numero dei passeggeri, i punti di partenza e arrivo, la durata e la lunghezza della corsa.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e7ac4-114">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="e7ac4-115">Il file **trip_fare.csv** contiene i dettagli della tariffa pagata per ciascuna corsa, ad esempio tipo di pagamento, importo, soprattassa e tasse, mance e pedaggi e l'importo totale pagato.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="e7ac4-116">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e7ac4-117">La **chiave univoca** usata per unire trip\_data e trip\_fare è costituita dai tre campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="e7ac4-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="e7ac4-118">medallion,</span></span>
* <span data-ttu-id="e7ac4-119">hack\_license e</span><span class="sxs-lookup"><span data-stu-id="e7ac4-119">hack\_license and</span></span>
* <span data-ttu-id="e7ac4-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-120">pickup\_datetime.</span></span>

## <span data-ttu-id="e7ac4-121"><a name="mltasks"></a>Risolvere tre tipi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="e7ac4-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="e7ac4-122">Sono stati formulati tre problemi di stima basati sul valore di *tip\_amount* per illustrare tre tipi di attività di modellazione:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="e7ac4-123">**Classificazione binaria**: consente di prevedere se sia stata lasciata o meno una mancia per la corsa. In questo caso, un valore di *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un valore di *tip\_amount* pari a $ 0 rappresenta un esempio negativo.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="e7ac4-124">**Classificazione multiclasse**: consente di prevedere l'intervallo in cui rientra la mancia lasciata per la corsa.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="e7ac4-125">Il valore *tip\_amount* viene suddiviso in cinque bin o classi:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="e7ac4-126">**Attività di regressione**: consente di prevedere l'importo della mancia lasciata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="e7ac4-127"><a name="setup"></a>Configurare l'ambiente di scienza dei dati di Azure per l'analisi avanzata</span><span class="sxs-lookup"><span data-stu-id="e7ac4-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="e7ac4-128">Per configurare l'ambiente di analisi scientifica dei dati di Azure, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="e7ac4-129">**Creare l'account di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="e7ac4-130">Quando si effettua il provisioning dell'archivio BLOB di Azure, scegliere una località geografica per l'archivio BLOB di Azure il più vicino possibile agli **Stati Uniti centro-meridionali**, dove vengono archiviati i dati relativi alle corse dei taxi di New York.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="e7ac4-131">I dati verranno copiati tramite AzCopy dal contenitore di archiviazione BLOB pubblico a un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="e7ac4-132">Quanto più l'archivio BLOB di Azure è vicino agli Stati Uniti centro-meridionali tanto più rapidamente verrà completata questa attività (passaggio 4).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="e7ac4-133">Per creare l'account di archiviazione di Azure, seguire i passaggi descritti in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e7ac4-134">Assicurarsi di prendere nota dei valori delle credenziali dell'account di archiviazione seguenti perché saranno necessarie più avanti nella procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="e7ac4-135">**Storage Account Name**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="e7ac4-136">**Chiave dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="e7ac4-137">**Nome contenitore** (in cui si vogliono salvare i dati nell'archivio BLOB di Azure)</span><span class="sxs-lookup"><span data-stu-id="e7ac4-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="e7ac4-138">**Effettuare il provisioning dell'istanza di Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="e7ac4-139">Per effettuare il provisioning di un'istanza di SQL Data Warehouse seguire la documentazione in [Creare un SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="e7ac4-140">Verificare di avere preso nota delle credenziali di SQL Data Warehouse seguenti che verranno usate nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="e7ac4-141">**Nome server**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="e7ac4-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="e7ac4-142">**Nome SQLDW (database)**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="e7ac4-143">**Nome utente**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-143">**Username**</span></span>
* <span data-ttu-id="e7ac4-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-144">**Password**</span></span>

<span data-ttu-id="e7ac4-145">**Installare Visual Studio e SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="e7ac4-146">Per istruzioni, vedere [Installare Visual Studio 2015 e SSDT per SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="e7ac4-147">**Connettersi ad Azure SQL DW con Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="e7ac4-148">Per istruzioni, vedere i passaggi 1 e 2 in [Connettersi ad Azure SQL Data Warehouse con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-149">Eseguire la query SQL seguente nel database creato in SQL Data Warehouse (anziché la query specificata nel passaggio 3 dell'argomento relativo alla connessione) per **creare una chiave master**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="e7ac4-150">**Creare un'area di lavoro di Azure Machine Learning nella sottoscrizione di Azure.**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="e7ac4-151">Per istruzioni, vedere [Creare un'area di lavoro di Machine Learning di Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="e7ac4-152"><a name="getdata"></a>Caricare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="e7ac4-153">Aprire una console dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="e7ac4-154">Eseguire i comandi di PowerShell seguenti per scaricare i file script SQL di esempio disponibili in GitHub in una directory locale specificata con il parametro *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="e7ac4-155">È possibile sostituire il valore del parametro *-DestDir* con quello di qualsiasi directory locale.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="e7ac4-156">Se *-DestDir* non esiste, verrà creata dallo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-157">Potrebbe essere necessario fare clic su **Esegui come amministratore** quando si esegue lo script di PowerShell seguente se sono richiesti privilegi di amministratore per creare o scrivere nella directory *DestDir* .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="e7ac4-158">Al termine dell'esecuzione, la directory di lavoro corrente diventa *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="e7ac4-159">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="e7ac4-160">In *-DestDir*eseguire lo script di PowerShell seguente in modalità amministratore:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="e7ac4-161">Quando lo script di PowerShell viene eseguito per la prima volta, verrà chiesto di inserire le informazioni da Azure SQL DW e dall'account di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="e7ac4-162">Quando l'esecuzione di questo script di PowerShell viene completata per la prima volta, le credenziali inserite risulteranno scritte in un file di configurazione SQLDW.conf nella directory di lavoro presente.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="e7ac4-163">L'esecuzione futura di questo file di script di PowerShell può leggere tutti i parametri necessari da questo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="e7ac4-164">Se è necessario modificare alcuni parametri, è possibile scegliere di inserirli nella schermata al prompt eliminando questo file di configurazione e inserendo i valori dei parametri come richiesto oppure di cambiare i valori dei parametri modificando il file SQLDW.conf nella directory *-DestDir* .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-165">Per evitare conflitti di nome schema con quelli già esistenti in Azure SQL DW, quando si leggono i parametri direttamente dal file SQLDW.conf, un numero casuale a 3 cifre viene aggiunto al nome schema dal file SQLDW.conf come nome schema predefinito per ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="e7ac4-166">Lo script di PowerShell può richiedere un nome schema: il nome può essere specificato a discrezione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="e7ac4-167">Questo file di **script di PowerShell** completa le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="e7ac4-168">**Esegue il download e l'installazione di AzCopy**, se non è già installato</span><span class="sxs-lookup"><span data-stu-id="e7ac4-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="e7ac4-169">**Copia i dati dal BLOB pubblico all'account di archiviazione BLOB privato** con AzCopy</span><span class="sxs-lookup"><span data-stu-id="e7ac4-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="e7ac4-170">**Carica i dati usando Polybase (eseguendo LoadDataToSQLDW.sql) in Azure SQL DW** dall'account di archiviazione BLOB privato tramite i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="e7ac4-171">Creare uno schema</span><span class="sxs-lookup"><span data-stu-id="e7ac4-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="e7ac4-172">Creare una credenziale con ambito di database</span><span class="sxs-lookup"><span data-stu-id="e7ac4-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="e7ac4-173">Creare un'origine dati esterna per un BLOB di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e7ac4-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="e7ac4-174">Creare un formato di file esterno da un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="e7ac4-175">I dati non sono compressi e i campi sono separati dal carattere barra verticale.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="e7ac4-176">Creare tabelle esterne relative a tariffe e corse per il set di dati relativo alle corse dei taxi di New York nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="e7ac4-177">Caricare dati dalle tabelle esterne nell'archivio BLOB di Azure in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="e7ac4-178">Creazione di una tabella dati di esempio (NYCTaxi_Sample) con inserimento di dati dalla selezione di query SQL sulle tabelle delle corse e delle tariffe.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="e7ac4-179">Per alcuni passaggi di questa procedura dettagliata deve essere usata la tabella di esempio.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="e7ac4-180">La posizione geografica degli account di archiviazione influisce sui tempi di caricamento.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-181">A seconda della posizione geografica dell'account di archiviazione BLOB privato, il processo di copia dei dati da un BLOB pubblico all'account di archiviazione privato può richiedere circa 15 minuti o anche di più e il processo di caricamento dei dati dall'account di archiviazione ad Azure SQL DW può richiedere 20 minuti o più.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="e7ac4-182">È necessario decidere cosa fare se si dispone di file di origine e destinazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-183">Se i file con estensione csv da copiare dall'archivio BLOB pubblico all'account di archiviazione BLOB privato esistono già nell'account di archiviazione BLOB privato, AzCopy chiederà se li si vuole sovrascrivere.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="e7ac4-184">Se non si vuole farlo, digitare **nn** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="e7ac4-185">Per sovrascriverli **tutti**, digitare **a** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="e7ac4-186">È anche possibile digitare **y** per sovrascrivere i file con estensione csv singolarmente.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Grafico n. 21][21]

<span data-ttu-id="e7ac4-188">È possibile usare i propri dati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-188">You can use your own data.</span></span> <span data-ttu-id="e7ac4-189">Se i dati sono nel computer locale nell'applicazione reale, è tuttavia possibile usare AzCopy per caricare i dati locali nell'archiviazione BLOB di Azure privato.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="e7ac4-190">È sufficiente sostituire il percorso **Source**, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, nel comando di AzCopy del file di script di PowerShell con la directory locale contenente i dati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="e7ac4-191">Se i dati sono già nell'archivio BLOB di Azure privato nell'applicazione reale, è possibile saltare il passaggio di AzCopy nello script di PowerShell e caricare direttamente i dati in Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="e7ac4-192">Saranno necessarie altre modifiche dello script per adattarlo al formato dei dati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="e7ac4-193">Questo script di PowerShell collega anche le informazioni di Azure SQL DW con i file di esempio di esplorazione dati SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py in modo che questi tre file possano essere provati subito al termine dello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="e7ac4-194">Al termine dell'esecuzione, verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="e7ac4-195"><a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e7ac4-196">In questa sezione vengono effettuate l'esplorazione dei dati e la generazione di funzionalità eseguendo query SQL direttamente su Azure SQL DW usando **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="e7ac4-197">Tutte le query SQL usate in questa sezione sono disponibili nello script di esempio *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="e7ac4-198">Questo file è già stato scaricato nella directory locale dallo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="e7ac4-199">È anche possibile recuperarlo da [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql),</span><span class="sxs-lookup"><span data-stu-id="e7ac4-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="e7ac4-200">ma al file in GitHub non sono collegate le informazioni di Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="e7ac4-201">Connettersi ad Azure SQL DW usando Visual Studio con il nome di accesso e la password di SQL DW e aprire **Esplora oggetti di SQL** per confermare che le tabelle e il database sono stati importati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="e7ac4-202">Recuperare il file *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ac4-203">Per aprire un editor di query Parallel Data Warehouse (PDW), usare il comando **Nuova query** mentre è selezionato PDW in **Esplora oggetti di SQL**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="e7ac4-204">L'editor di query SQL standard non è supportato da PDW.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="e7ac4-205">Ecco il tipo di attività di esplorazione dei dati e di generazione di funzionalità eseguite in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="e7ac4-206">Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="e7ac4-207">Indagine sulla qualità dei dati dei campi di longitudine e latitudine.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="e7ac4-208">Generazione di etichette di classificazione binaria e multiclasse basata su **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="e7ac4-209">Generazione di funzionalità calcolo/confronto delle distanze delle corse.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="e7ac4-210">Unione di due tabelle ed estrazione di un campione casuale che verrà utilizzato per la creazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="e7ac4-211">Verifica dell'importazione dei dati</span><span class="sxs-lookup"><span data-stu-id="e7ac4-211">Data import verification</span></span>
<span data-ttu-id="e7ac4-212">Queste query consentono una verifica rapida del numero di righe e di colonne nelle tabelle popolate in precedenza tramite l'importazione in blocco in parallelo di Polybase,</span><span class="sxs-lookup"><span data-stu-id="e7ac4-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="e7ac4-213">**Output:** si dovrebbero ottenere 173.179.759 righe e 14 colonne.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="e7ac4-214">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e7ac4-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="e7ac4-215">Questa query di esempio identifica le licenze (numeri dei taxi) che hanno eseguito più di 100 corse in un periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="e7ac4-216">Per la query verrà usata la tabella partizionata poiché è condizionata dallo schema di partizione di **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="e7ac4-217">Per la query del set di dati completo verrà inoltre utilizzata la tabella partizionata e/o l'analisi dell'indice.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="e7ac4-218">**Output:** la query dovrebbe restituire una tabella con righe che specificano le 13.369 licenze (taxi) e il numero di viaggi eseguiti da ognuna nel 2013.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="e7ac4-219">L'ultima colonna contiene il totale delle corse eseguite.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="e7ac4-220">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="e7ac4-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="e7ac4-221">Questo esempio identifica le licenze (numeri dei taxi) e i numeri di hack_license (tassisti) che hanno eseguito più di 100 corse in un periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="e7ac4-222">**Output:** la query dovrebbe restituire una tabella con 13.369 righe in cui vengono specificati quali dei 13.369 ID di automobile/autista hanno eseguito più di 100 corse nel 2013.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="e7ac4-223">L'ultima colonna contiene il totale delle corse eseguite.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="e7ac4-224">Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate</span><span class="sxs-lookup"><span data-stu-id="e7ac4-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="e7ac4-225">In questo esempio viene esaminato se uno dei campi relativi alla longitudine o alla latitudine contiene un valore non valido (i gradi radianti devono essere compresi tra -90 e 90) o presenta le coordinate (0, 0).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="e7ac4-226">**Output:** la query restituisce 837.467 corse i cui campi longitudine e/o latitudine non sono validi.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="e7ac4-227">Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="e7ac4-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="e7ac4-228">Questo esempio trova il numero di corse per cui è stata lasciata una mancia rispetto a quelle per cui non è stata lasciata una mancia in un periodo specificato oppure nel set di dati completo, se copre tutto l'anno (come in questo caso).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="e7ac4-229">Questa distribuzione riflette la distribuzione delle etichette binarie che dovranno essere utilizzate in seguito per la creazione di modelli di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="e7ac4-230">**Output:** la query dovrebbe restituire le frequenze di mance seguenti per l'anno 2013: 90.447.622 corse per cui è stata lasciata una mancia e 82.264.709 corse per cui non è stata lasciata una mancia.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="e7ac4-231">Esplorazione: distribuzione della classe o dell'intervallo delle mance</span><span class="sxs-lookup"><span data-stu-id="e7ac4-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="e7ac4-232">In questo esempio viene calcolata la distribuzione degli intervalli delle mance in un determinato periodo (o nel set di dati completo, in caso di un anno intero).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="e7ac4-233">Si tratta della distribuzione delle classi di etichette che verranno utilizzate in seguito per la creazione di modelli di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="e7ac4-234">**Output:**</span><span class="sxs-lookup"><span data-stu-id="e7ac4-234">**Output:**</span></span>

| <span data-ttu-id="e7ac4-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="e7ac4-235">tip_class</span></span> | <span data-ttu-id="e7ac4-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="e7ac4-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="e7ac4-237">1</span><span class="sxs-lookup"><span data-stu-id="e7ac4-237">1</span></span> |<span data-ttu-id="e7ac4-238">82230915</span><span class="sxs-lookup"><span data-stu-id="e7ac4-238">82230915</span></span> |
| <span data-ttu-id="e7ac4-239">2</span><span class="sxs-lookup"><span data-stu-id="e7ac4-239">2</span></span> |<span data-ttu-id="e7ac4-240">6198803</span><span class="sxs-lookup"><span data-stu-id="e7ac4-240">6198803</span></span> |
| <span data-ttu-id="e7ac4-241">3</span><span class="sxs-lookup"><span data-stu-id="e7ac4-241">3</span></span> |<span data-ttu-id="e7ac4-242">1932223</span><span class="sxs-lookup"><span data-stu-id="e7ac4-242">1932223</span></span> |
| <span data-ttu-id="e7ac4-243">0</span><span class="sxs-lookup"><span data-stu-id="e7ac4-243">0</span></span> |<span data-ttu-id="e7ac4-244">82264625</span><span class="sxs-lookup"><span data-stu-id="e7ac4-244">82264625</span></span> |
| <span data-ttu-id="e7ac4-245">4</span><span class="sxs-lookup"><span data-stu-id="e7ac4-245">4</span></span> |<span data-ttu-id="e7ac4-246">85765</span><span class="sxs-lookup"><span data-stu-id="e7ac4-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="e7ac4-247">Esplorazione: calcolo e confronto della distanza delle corse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="e7ac4-248">In questo esempio, la longitudine e la latitudine del prelievo e dello scarico vengono convertite in punti geografici SQL, viene calcolata la distanza della corsa mediante la differenza dei punti geografici di SQL e viene restituito un campione casuale dei risultati per il confronto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="e7ac4-249">Nell'esempio i risultati vengono limitati unicamente alle coordinate valide tramite la query per la valutazione della qualità dei dati illustrata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="e7ac4-250">Progettazione di funzionalità con le funzioni SQL</span><span class="sxs-lookup"><span data-stu-id="e7ac4-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="e7ac4-251">Le funzioni SQL a volte possono essere una valida opzione per progettare funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="e7ac4-252">In questa procedura dettagliata viene definita una funzione SQL per calcolare la distanza diretta tra le località di partenza e di arrivo.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="e7ac4-253">È possibile eseguire gli script SQL seguenti in **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="e7ac4-254">Ecco lo script SQL che definisce la funzione della distanza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="e7ac4-255">Ecco un esempio per chiamare questa funzione per generare le funzionalità nella query SQL:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="e7ac4-256">**Output:** questa query genera una tabella (con 2.803.538 righe) con la latitudine e la longitudine del prelievo e dello scarico e le corrispondenti distanze dirette in miglia.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="e7ac4-257">Di seguito sono riportati i risultati delle prime 3 righe:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="e7ac4-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="e7ac4-258">pickup_latitude</span></span> | <span data-ttu-id="e7ac4-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="e7ac4-259">pickup_longitude</span></span> | <span data-ttu-id="e7ac4-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="e7ac4-260">dropoff_latitude</span></span> | <span data-ttu-id="e7ac4-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="e7ac4-261">dropoff_longitude</span></span> | <span data-ttu-id="e7ac4-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="e7ac4-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e7ac4-263">1</span><span class="sxs-lookup"><span data-stu-id="e7ac4-263">1</span></span> |<span data-ttu-id="e7ac4-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="e7ac4-264">40.731804</span></span> |<span data-ttu-id="e7ac4-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="e7ac4-265">-74.001083</span></span> |<span data-ttu-id="e7ac4-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="e7ac4-266">40.736622</span></span> |<span data-ttu-id="e7ac4-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="e7ac4-267">-73.988953</span></span> |<span data-ttu-id="e7ac4-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="e7ac4-268">.7169601222</span></span> |
| <span data-ttu-id="e7ac4-269">2</span><span class="sxs-lookup"><span data-stu-id="e7ac4-269">2</span></span> |<span data-ttu-id="e7ac4-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="e7ac4-270">40.715794</span></span> |<span data-ttu-id="e7ac4-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="e7ac4-271">-74,010635</span></span> |<span data-ttu-id="e7ac4-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="e7ac4-272">40.725338</span></span> |<span data-ttu-id="e7ac4-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="e7ac4-273">-74.00399</span></span> |<span data-ttu-id="e7ac4-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="e7ac4-274">.7448343721</span></span> |
| <span data-ttu-id="e7ac4-275">3</span><span class="sxs-lookup"><span data-stu-id="e7ac4-275">3</span></span> |<span data-ttu-id="e7ac4-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="e7ac4-276">40.761456</span></span> |<span data-ttu-id="e7ac4-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="e7ac4-277">-73.999886</span></span> |<span data-ttu-id="e7ac4-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="e7ac4-278">40.766544</span></span> |<span data-ttu-id="e7ac4-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="e7ac4-279">-73.988228</span></span> |<span data-ttu-id="e7ac4-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="e7ac4-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="e7ac4-281">Preparazione dei dati per la creazione del modello</span><span class="sxs-lookup"><span data-stu-id="e7ac4-281">Prepare data for model building</span></span>
<span data-ttu-id="e7ac4-282">Le query riportate di seguito consentono di unire le tabelle **nyctaxi\_trip** e **nyctaxi\_fare**, generare un'etichetta di classificazione binaria **tipped**, un'etichetta di classificazione multiclasse **tip\_class** e di estrarre un campione dall'intero set di dati unito.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="e7ac4-283">Il campionamento viene eseguito recuperando un subset delle corse in base all'orario di partenza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="e7ac4-284">La query può essere copiata e incollata direttamente nel modulo [Import Data][import-data] (Importa dati) di [Azure Machine Learning Studio](https://studio.azureml.net) per l'inserimento diretto dei dati dall'istanza del database SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="e7ac4-285">La query esclude i record con le coordinate errate (0, 0).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="e7ac4-286">Una volta pronti a proseguire con Azure Machine Learning, è possibile effettuare una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="e7ac4-287">Salvare la query SQL finale per estrarre e campionare i dati e copiare e incollare la query direttamente in un modulo [Import Data][import-data] (Importa dati) in Azure Machine Learning, oppure</span><span class="sxs-lookup"><span data-stu-id="e7ac4-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="e7ac4-288">Salvare in modo definitivo i dati campionati e progettati che si prevede di usare per la compilazione di modelli in una nuova tabella di SQL DW e usare la nuova tabella nel modulo [Import Data][import-data] (Importa dati) in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="e7ac4-289">Questa operazione è stata eseguita dallo script di PowerShell nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="e7ac4-290">È possibile leggere direttamente in questa tabella nel modulo Import Data.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="e7ac4-291"><a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e7ac4-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="e7ac4-292">In questa sezione verranno eseguite l'esplorazione dei dati e la generazione di funzionalità usando query sia Python che SQL sull'istanza di SQL DW creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="e7ac4-293">Un IPython Notebook di esempio denominato **SQLDW_Explorations.ipynb** e un file di script di Python **SQLDW_Explorations_Scripts.py** sono stati scaricati nella directory locale.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="e7ac4-294">Sono disponibili anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="e7ac4-295">Questi due file sono identici negli script di Python.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="e7ac4-296">Il file di script di Python viene fornito nel caso in cui non sia presente un server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="e7ac4-297">Questi due file di Python di esempio sono stati progettati in **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="e7ac4-298">Le informazioni di Azure SQL DW necessarie nell'esempio di IPython Notebook e il file di script di Python scaricati nel computer locale sono stati collegati prima dallo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="e7ac4-299">Possono essere eseguiti senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-299">They are executable without any modification.</span></span>

<span data-ttu-id="e7ac4-300">Se si è già configurata un'area di lavoro di AzureML, è possibile caricare direttamente l'esempio di IPython Notebook nel servizio IPython Notebook di AzureML e avviarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="e7ac4-301">Ecco i passaggi per caricare il servizio IPython Notebook di AzureML:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="e7ac4-302">Accedere all'area di lavoro AzureML, fare clic su "Studio" in alto e fare clic su "NOTEBOOKS" a sinistra nella pagina Web.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Grafico n. 22][22]
2. <span data-ttu-id="e7ac4-304">Fare clic su "NEW" nell'angolo in basso a sinistra della pagina Web e selezionare "Python 2".</span><span class="sxs-lookup"><span data-stu-id="e7ac4-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="e7ac4-305">Specificare quindi un nome per il notebook e fare clic sul segno di spunta per creare il nuovo IPython Notebook vuoto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Grafico n. 23][23]
3. <span data-ttu-id="e7ac4-307">Fare clic sul simbolo "Jupyter" nell'angolo in alto a sinistra del nuovo IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Grafico n. 24][24]
4. <span data-ttu-id="e7ac4-309">Trascinare l'esempio di IPython Notebook nella pagina **albero** del servizio IPython Notebook di Azure Machine Learning e fare clic su **Upload** (Carica).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="e7ac4-310">L'esempio di IPython Notebook verrà quindi caricato nel servizio IPython Notebook di AzureML.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Grafico n. 25][25]

<span data-ttu-id="e7ac4-312">Per eseguire l'esempio di IPython Notebook o il file di script di Python, sono necessari i pacchetti di Python seguenti.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="e7ac4-313">Se si usa il servizio IPython Notebook di AzureML, questi pacchetti sono stati preinstallati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="e7ac4-314">pandas</span><span class="sxs-lookup"><span data-stu-id="e7ac4-314">pandas</span></span>
    - <span data-ttu-id="e7ac4-315">numpy</span><span class="sxs-lookup"><span data-stu-id="e7ac4-315">numpy</span></span>
    - <span data-ttu-id="e7ac4-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="e7ac4-316">matplotlib</span></span>
    - <span data-ttu-id="e7ac4-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="e7ac4-317">pyodbc</span></span>
    - <span data-ttu-id="e7ac4-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="e7ac4-318">PyTables</span></span>

<span data-ttu-id="e7ac4-319">La sequenza consigliata quando si compilano soluzioni analitiche avanzate in AzureML con dati di grandi dimensioni è la seguente:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="e7ac4-320">Leggere un piccolo campione di dati in un frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="e7ac4-321">Eseguire alcune visualizzazioni ed esplorazioni tramite i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="e7ac4-322">Sperimentare la progettazione di funzionalità utilizzando i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="e7ac4-323">Per operazioni più estese di esplorazione dei dati, manipolazione dei dati e progettazione di funzionalità, usare Python per inviare query SQL direttamente a SQL DW.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="e7ac4-324">Decidere la dimensione del campione adatta per la creazione di modelli di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="e7ac4-325">Di seguito vengono forniti alcuni esempi di esplorazione dei dati, visualizzazione dei dati e progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="e7ac4-326">Altre esplorazioni dei dati sono disponibili nell'esempio di IPython Notebook e nel file di script di Python di esempio.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="e7ac4-327">Inizializzare le credenziali di database</span><span class="sxs-lookup"><span data-stu-id="e7ac4-327">Initialize database credentials</span></span>
<span data-ttu-id="e7ac4-328">Inizializzare le impostazioni di connessione del database nelle seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="e7ac4-329">Creare la connessione al database</span><span class="sxs-lookup"><span data-stu-id="e7ac4-329">Create database connection</span></span>
<span data-ttu-id="e7ac4-330">Ecco la stringa di connessione che crea la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="e7ac4-331">Segnalare il numero di righe e di colonne nella tabella <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="e7ac4-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="e7ac4-332">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="e7ac4-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="e7ac4-333">Numero di colonne totali = 14</span><span class="sxs-lookup"><span data-stu-id="e7ac4-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="e7ac4-334">Segnalare il numero di righe e di colonne nella tabella <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="e7ac4-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="e7ac4-335">Numero di righe totali = 173179759</span><span class="sxs-lookup"><span data-stu-id="e7ac4-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="e7ac4-336">Numero di colonne totali = 11</span><span class="sxs-lookup"><span data-stu-id="e7ac4-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="e7ac4-337">Leggere un piccolo campione di dati dal database SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="e7ac4-338">Il tempo per la lettura della tabella di esempio è di 14,096495 secondi.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="e7ac4-339">Numero di righe e di colonne recuperate = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="e7ac4-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="e7ac4-340">Statistiche descrittive</span><span class="sxs-lookup"><span data-stu-id="e7ac4-340">Descriptive statistics</span></span>
<span data-ttu-id="e7ac4-341">Ora è possibile esplorare i dati campionati.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="e7ac4-342">Si inizia da alcune statistiche descrittive per **trip\_distance** (o qualsiasi altro campo che si sceglie di specificare).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="e7ac4-343">Visualizzazione: esempio di box plot</span><span class="sxs-lookup"><span data-stu-id="e7ac4-343">Visualization: Box plot example</span></span>
<span data-ttu-id="e7ac4-344">Successivamente si consulterà il box plot per la distanza delle corse, per visualizzare i quantili.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="e7ac4-346">Visualizzazione: esempio di tracciato di distribuzione</span><span class="sxs-lookup"><span data-stu-id="e7ac4-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="e7ac4-347">Tracciati che visualizzano la distribuzione e un istogramma per le distanze delle corse campionate.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="e7ac4-349">Visualizzazione: tracciati a barre e linee</span><span class="sxs-lookup"><span data-stu-id="e7ac4-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="e7ac4-350">In questo esempio, la distanza delle corse viene suddivisa in cinque contenitori e vengono visualizzati i risultati di questa suddivisione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="e7ac4-351">La distribuzione binaria precedente può essere rappresentata in un tracciato a barre o linee con:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

<span data-ttu-id="e7ac4-353">e</span><span class="sxs-lookup"><span data-stu-id="e7ac4-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="e7ac4-355">Visualizzazione: esempi di grafico a dispersione</span><span class="sxs-lookup"><span data-stu-id="e7ac4-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="e7ac4-356">Viene eseguito un grafico a dispersione tra **trip\_time\_in\_secs** e **trip\_distance** per verificare se esiste una correlazione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

<span data-ttu-id="e7ac4-358">Allo stesso modo, è possibile verificare la relazione tra **rate\_code** e **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="e7ac4-360">Esplorazione nei dati campionati usando query SQL in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="e7ac4-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="e7ac4-361">In questa sezione verranno esplorate le distribuzioni di dati usando i dati campionati salvati in modo definitivo nella nuova tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="e7ac4-362">Si noti che esplorazioni simili possono essere eseguite usando le tabelle originali.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="e7ac4-363">Esplorazione: segnalare il numero di righe e di colonne nella tabella campionata</span><span class="sxs-lookup"><span data-stu-id="e7ac4-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="e7ac4-364">Esplorazione: distribuzione delle corse per cui è stata lasciata una mancia e di quelle per cui non è stata lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="e7ac4-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="e7ac4-365">Esplorazione: distribuzione della classe delle mance</span><span class="sxs-lookup"><span data-stu-id="e7ac4-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="e7ac4-366">Esplorazione: tracciare la distribuzione delle mance per classe</span><span class="sxs-lookup"><span data-stu-id="e7ac4-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Grafico n. 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="e7ac4-368">Esplorazione: distribuzione giornaliera delle corse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="e7ac4-369">Esplorazione: distribuzione delle corse per licenza</span><span class="sxs-lookup"><span data-stu-id="e7ac4-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="e7ac4-370">Esplorazione: distribuzione delle corse per licenza e hack_license</span><span class="sxs-lookup"><span data-stu-id="e7ac4-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="e7ac4-371">Esplorazione: distribuzione degli orari delle corse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="e7ac4-372">Esplorazione: distribuzione delle distanze delle corse</span><span class="sxs-lookup"><span data-stu-id="e7ac4-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="e7ac4-373">Esplorazione: distribuzione dei tipi di pagamento</span><span class="sxs-lookup"><span data-stu-id="e7ac4-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="e7ac4-374">Verificare l'aspetto finale della tabella con funzionalità</span><span class="sxs-lookup"><span data-stu-id="e7ac4-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="e7ac4-375"><a name="mlmodel"></a>Creare modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e7ac4-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="e7ac4-376">A questo punto è possibile procedere con la creazione e la distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="e7ac4-377">I dati sono pronti per essere usati nei problemi di stima identificati in precedenza, in modo specifico:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="e7ac4-378">**Classificazione binaria**: consente di prevedere se per la corsa è stata lasciata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="e7ac4-379">**Classificazione multiclasse**: consente di prevedere l'intervallo di mance pagato, in base alle classi definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="e7ac4-380">**Attività di regressione**: consente di prevedere l'importo della mancia lasciata per una corsa.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="e7ac4-381">Per iniziare l'esercizio relativo alla creazione di modelli, accedere all'area di lavoro **Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="e7ac4-382">Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure ML](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="e7ac4-383">Per iniziare a utilizzare Azure Machine Learning, vedere [Informazioni su Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="e7ac4-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="e7ac4-384">Effettuare l'accesso ad [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="e7ac4-385">Nella pagina iniziale vengono fornite moltissime informazioni, video, esercitazioni, collegamenti al Riferimento ai moduli e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="e7ac4-386">Per altre informazioni su Azure Machine Learning, consultare il [Centro di documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="e7ac4-387">Un tipico esperimento di training comprende i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="e7ac4-388">Creazione di un esperimento **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="e7ac4-389">Inserimento dei dati in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="e7ac4-390">Pre-elaborazione, trasformazione e manipolazione dei dati secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="e7ac4-391">Generazione di funzionalità, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-391">Generate features as needed.</span></span>
5. <span data-ttu-id="e7ac4-392">Suddivisione dei dati in set di dati di training, convalida o test(o creazione di set di dati distinti per ciascuna tipologia).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="e7ac4-393">Selezione di uno o più algoritmi Machine Learning, a seconda del problema di apprendimento da risolvere.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="e7ac4-394">Ad esempio, classificazione binaria, classificazione multiclasse, regressione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="e7ac4-395">Training di uno o più modelli tramite il set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="e7ac4-396">Calcolo del punteggio del set di dati di convalida mediante i modelli sottoposti a training.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="e7ac4-397">Valutazione dei modelli per calcolare la metrica rilevante per il problema di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="e7ac4-398">Ottimizzazione dei modelli e selezione del modello migliore per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="e7ac4-399">In questo esercizio i dati sono già stati esplorati e compilati in SQL Data Warehouse ed è stata decisa la dimensione del campione da inserire in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="e7ac4-400">Ecco la procedura per compilare uno o più modelli di stima:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="e7ac4-401">Inserire i dati in Azure ML tramite il modulo [Import Data][import-data] (Importa dati) , disponibile nella sezione **Data Input and Output** (Input e output dei dati).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="e7ac4-402">Per altre informazioni, vedere la pagina di riferimento sul modulo [Import Data][import-data] (Importa Dati).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Import Data di Azure ML][17]
2. <span data-ttu-id="e7ac4-404">Selezionare **Azure SQL Database** (Database SQL Azure) come **Data source** (Origine dati) nel riquadro **Properties** (Proprietà).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="e7ac4-405">Immissione del nome DNS del database nel campo **Nome server database** .</span><span class="sxs-lookup"><span data-stu-id="e7ac4-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="e7ac4-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="e7ac4-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="e7ac4-407">Immissione del **Nome database** nel campo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="e7ac4-408">Immettere il *nome utente SQL* in **Server user account name** (Nome account utente server) e la *password* in **Server user account password** (Password account utente server).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="e7ac4-409">Fare clic sull'opzione **Accept any server certificate** (Accetta qualsiasi certificato server).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="e7ac4-410">Nell'area di testo di modifica **Query database** , incollare la query che consente di estrarre i campi di database necessari (inclusi i campi calcolati come le etichette) e sottocampionare i dati nella dimensione campione desiderata.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="e7ac4-411">Nella figura seguente è illustrato un esempio di esperimento di classificazione binaria per la lettura dei dati direttamente dal database SQL Data Warehouse. Si ricordi di sostituire i nomi delle tabelle nyctaxi_trip e nyctaxi_fare con il nome schema e i nomi delle tabelle usati nella procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="e7ac4-412">È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formazione su Azure ML][10]

> [!IMPORTANT]
> <span data-ttu-id="e7ac4-414">Negli esempi di estrazione dei dati di modellazione e di query di campionamento forniti nelle sezioni precedenti, **tutte le etichette per i tre esercizi sulla creazione dei modelli sono incluse nella query**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="e7ac4-415">Un passaggio importante (richiesto) in ciascun esercizio sulla modellazione consiste nell'**escludere** le etichette non necessarie per gli altri due problemi ed eventuali **perdite di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="e7ac4-416">Ad esempio, con la classificazione binaria, usare l'etichetta **tipped** ed escludere i campi **tip\_class**, **tip\_amount** e **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="e7ac4-417">Questi ultimi sono perdite di destinazione in quanto implicano la mancia pagata.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="e7ac4-418">Per escludere eventuali colonne non necessarie o le perdite di destinazione, è possibile usare il modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) o [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="e7ac4-419">Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="e7ac4-420"><a name="mldeploy"></a>Distribuire modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e7ac4-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="e7ac4-421">Quando il modello è pronto, è possibile distribuirlo in modo semplice come servizio Web direttamente dall'esperimento.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="e7ac4-422">Per ulteriori informazioni sulla distribuzione di servizi Web Azure ML, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="e7ac4-423">Per distribuire un nuovo servizio Web, è necessario effettuare le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="e7ac4-424">Creare un esperimento di assegnazione di punteggio.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="e7ac4-425">Distribuire il servizio web.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-425">Deploy the web service.</span></span>

<span data-ttu-id="e7ac4-426">Per creare un esperimento di assegnazione dei punteggi da un esperimento di training **completato**, fare clic su **CREATE SCORING EXPERIMENT** (CREA ESPERIMENTO DI ASSEGNAZIONE PUNTEGGI) nella barra delle azioni inferiore.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Valutazione di Azure][18]

<span data-ttu-id="e7ac4-428">Azure Machine Learning tenterà di creare un esperimento di assegnazione di punteggio basato sui componenti dell'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="e7ac4-429">In particolare, verranno effettuate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e7ac4-429">In particular, it will:</span></span>

1. <span data-ttu-id="e7ac4-430">Salvataggio del modello sottoposto a training e rimozione dei moduli di training del modello.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="e7ac4-431">Identificazione di una **porta di input** logica per rappresentare lo schema di dati di input previsto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="e7ac4-432">Identificazione di una **porta di output** logica per rappresentare lo schema di output del servizio Web previsto.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="e7ac4-433">Una volta creato l'esperimento di punteggio, esaminarlo e apportare le dovute modifiche.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="e7ac4-434">Una regolazione tipica consiste nel sostituire il set di dati di input e/o la query con uno che escluda i campi etichetta, in quanto questi non saranno disponibili quando si chiama il servizio.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="e7ac4-435">È inoltre buona norma ridurre la dimensione del set di dati di input e/o della query a pochi record, sufficienti a indicare lo schema di input.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="e7ac4-436">Per la porta di output, di solito vengono esclusi tutti i campi di input e inclusi soltanto **Scored Labels** (Etichette con punteggio) e **Scored Probabilities** (Probabilità con punteggio) nell'output, tramite il modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="e7ac4-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e7ac4-437">Nella figura di seguito viene fornito un esperimento di assegnazione dei punteggi di esempio.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="e7ac4-438">Quando si è pronti per la distribuzione, fare clic sul pulsante **PUBBLICA SERVIZIO WEB** nella barra delle azioni inferiore.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Pubblicazione di Azure ML][11]

## <a name="summary"></a><span data-ttu-id="e7ac4-440">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e7ac4-440">Summary</span></span>
<span data-ttu-id="e7ac4-441">Ricapitolando quanto è stato fatto, durante questa procedura è stato creato un ambiente di analisi scientifica dei dati di Azure da usare con set di dati pubblici di grandi dimensioni, seguendo l'intero Processo di analisi scientifica dei dati per i team, dall'acquisizione dei dati al training del modello e quindi alla distribuzione di un servizio Web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="e7ac4-442">Informazioni sulla licenza</span><span class="sxs-lookup"><span data-stu-id="e7ac4-442">License information</span></span>
<span data-ttu-id="e7ac4-443">Questa procedura dettagliata di esempio e gli script e i blocchi di appunti IPython che la accompagnano sono condivisi da Microsoft nella licenza MIT.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="e7ac4-444">Selezionare il file LICENSE.txt nella directory del codice di esempio in GitHub per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="e7ac4-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="e7ac4-445">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="e7ac4-445">References</span></span>
<span data-ttu-id="e7ac4-446">•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="e7ac4-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="e7ac4-447">•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="e7ac4-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="e7ac4-448">•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="e7ac4-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
