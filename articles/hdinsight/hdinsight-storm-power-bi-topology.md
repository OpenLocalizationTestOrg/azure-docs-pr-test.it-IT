---
title: 'Usare Apache Storm con Power BI: Azure HDInsight | Microsoft Docs'
description: Creare un report di Power BI con i dati da una topologia C# in esecuzione in un cluster Apache Storm in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="dd1c1-103">Usare Power BI per visualizzare i dati provenienti da una topologia Apache Storm</span><span class="sxs-lookup"><span data-stu-id="dd1c1-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="dd1c1-104">Power BI consente di mostrare visivamente i dati sotto forma di report.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="dd1c1-105">Questo documento fornisce un esempio dell'uso di Apache Storm in HDInsight per la generazione di dati per Power BI.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="dd1c1-106">La procedura illustrata in questo documento si basa su un ambiente di sviluppo Windows con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="dd1c1-107">Il progetto compilato può essere inviato a un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dd1c1-108">Solo i cluster basati su Linux creati dopo il 28/10/2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="dd1c1-109">Per usare una topologia C# con un cluster basato su Linux, aggiornare il pacchetto NuGet Microsoft.SCP.Net.SDK usato dal progetto alla versione 0.10.0.6 o successiva.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="dd1c1-110">La versione del pacchetto deve anche corrispondere alla versione principale di Storm installata in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="dd1c1-111">Ad esempio, le versioni 3.3 e 3.4 di Storm in HDInsight usano Storm versione 0.10.x, mentre HDInsight 3.5 usa Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="dd1c1-112">Le topologie C# nei cluster basati su Linux devono usare .NET 4.5 e devono usare Mono per l'esecuzione nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="dd1c1-113">Anche se non dovrebbero verificarsi problemi,</span><span class="sxs-lookup"><span data-stu-id="dd1c1-113">Most things work.</span></span> <span data-ttu-id="dd1c1-114">è consigliabile vedere il documento [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Compatibilità di Mono) per potenziali incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="dd1c1-115">Per una versione Java di questo progetto, che funziona con HDInsight basato su Linux o Windows, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd1c1-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd1c1-116">Prerequisites</span></span>

* <span data-ttu-id="dd1c1-117">Un utente di Azure Active Directory con accesso [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="dd1c1-118">Un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-118">An HDInsight cluster.</span></span> <span data-ttu-id="dd1c1-119">Per altre informazioni, vedere [Introduzione a Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dd1c1-120">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dd1c1-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="dd1c1-122">Visual Studio (una delle versioni seguenti)</span><span class="sxs-lookup"><span data-stu-id="dd1c1-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="dd1c1-123">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="dd1c1-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="dd1c1-124">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="dd1c1-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="dd1c1-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="dd1c1-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="dd1c1-126">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="dd1c1-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="dd1c1-127">Gli strumenti HDInsight per Visual Studio. Per informazioni sull'installazione, vedere [Introduzione all'uso di HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="dd1c1-128">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="dd1c1-128">How it works</span></span>

<span data-ttu-id="dd1c1-129">Questo esempio contiene una topologia Storm C# che genera in modo casuale i dati di log di Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="dd1c1-130">I dati vengono quindi scritti in un database SQL e da qui vengono usati per generare report in Power BI.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="dd1c1-131">I file seguenti implementano la funzionalità principale di questo esempio:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="dd1c1-132">**SqlAzureBolt.cs**: scrive nel database SQL le informazioni generate nella topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="dd1c1-133">**IISLogsTable.sql**: istruzioni Transact-SQL usate per generare il database in cui vengono archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="dd1c1-134">Creare la tabella nel database SQL prima di avviare la topologia nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="dd1c1-135">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="dd1c1-135">Download the example</span></span>

<span data-ttu-id="dd1c1-136">Scaricare l' [esempio di Power BI per C# Storm in HDInsight](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="dd1c1-137">Per scaricarlo, biforcarlo o clonarlo mediante [git](http://git-scm.com/)oppure usare il collegamento **Download** per scaricare un file con estensione zip dell'archivio.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="dd1c1-138">Creare un database</span><span class="sxs-lookup"><span data-stu-id="dd1c1-138">Create a database</span></span>

1. <span data-ttu-id="dd1c1-139">Per creare un database, seguire la procedura riportata nel documento [Esercitazione sul database SQL](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="dd1c1-140">Connettersi al database seguendo la procedura riportata nel documento [Connettersi a un database SQL con Visual Studio](../sql-database/sql-database-connect-query.md).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="dd1c1-141">In Esplora oggetti fare clic con il pulsante destro del mouse sul database e scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="dd1c1-142">Incollare il contenuto del file **IISLogsTable.sql** incluso nel progetto scaricato nella finestra di query e quindi usare CTRL+MAIUSC+E per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="dd1c1-143">Verrà visualizzato un messaggio per informare che i comandi sono stati eseguiti correttamente.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="dd1c1-144">Configurare l'esempio</span><span class="sxs-lookup"><span data-stu-id="dd1c1-144">Configure the sample</span></span>

1. <span data-ttu-id="dd1c1-145">Nel [portale di Azure](https://portal.azure.com)selezionare il database SQL.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="dd1c1-146">Nella sezione **Informazioni di base** del pannello Database SQL selezionare **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="dd1c1-147">Nell'elenco visualizzato copiare le informazioni relative a **ADO.NET (autenticazione SQL)** .</span><span class="sxs-lookup"><span data-stu-id="dd1c1-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="dd1c1-148">Aprire l'esempio in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="dd1c1-149">In **Esplora soluzioni** aprire il file **App.config** e quindi trovare la voce seguente:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="dd1c1-150">Sostituire il valore **##TOBEFILLED##** con la stringa di connessione del database copiata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="dd1c1-151">Sostituire **{your\_username}** e **{your\_password}** con il nome utente e la password per il database.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="dd1c1-152">Salvare e chiudere i file.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="dd1c1-153">Distribuire l'esempio</span><span class="sxs-lookup"><span data-stu-id="dd1c1-153">Deploy the sample</span></span>

1. <span data-ttu-id="dd1c1-154">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **StormToSQL** e quindi scegliere **Submit to Storm on HDInsight** (Invia a Storm in HDInsight).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="dd1c1-155">Selezionare il cluster HDInsight dall'elenco a discesa **Cluster Storm** .</span><span class="sxs-lookup"><span data-stu-id="dd1c1-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd1c1-156">Il popolamento dell'elenco a discesa **Cluster Storm** con i nomi dei server potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="dd1c1-157">Se richiesto, immettere le credenziali di accesso per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="dd1c1-158">Se si dispone di più di una sottoscrizione, accedere a quella che contiene il cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="dd1c1-159">Dopo l'invio della topologia, verrà aperto __Storm Topologies Viewer__ (Visualizzatore topologie Storm).</span><span class="sxs-lookup"><span data-stu-id="dd1c1-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="dd1c1-160">Per visualizzare la topologia, selezionare dall'elenco la voce SqlAzureWriterTopology.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Topologie con la topologia selezionata](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="dd1c1-162">È possibile usare questa visualizzazione per ottenere informazioni sulla topologia. In alternativa, fare doppio clic su una voce, ad esempio SqlAzureBolt, per visualizzare informazioni specifiche di un componente della topologia.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="dd1c1-163">Dopo l'esecuzione della topologia per alcuni minuti, tornare alla finestra di query SQL usata per creare il database.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="dd1c1-164">Sostituire le istruzioni esistenti con la query seguente:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="dd1c1-165">Usare CTRL+MAIUSC+E per eseguire la query. Verranno visualizzati risultati simili ai dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="dd1c1-166">Si tratta di dati scritti dalla topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="dd1c1-167">Creare un report</span><span class="sxs-lookup"><span data-stu-id="dd1c1-167">Create a report</span></span>

1. <span data-ttu-id="dd1c1-168">Connettersi al [connettore Database SQL di Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) per Power BI.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="dd1c1-169">In **Database** selezionare **Recupera**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="dd1c1-170">Selezionare **Database SQL di Azure** e quindi **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd1c1-171">Potrebbe essere richiesto di scaricare Power BI Desktop per continuare.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="dd1c1-172">In tal caso, seguire questa procedura per connettersi:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="dd1c1-173">Aprire Power BI Desktop e selezionare __Recupera dati__.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="dd1c1-174">2 Selezionare __Azure__ e quindi __Database SQL di Azure__.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="dd1c1-175">Immettere le informazioni per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="dd1c1-176">È possibile trovare queste informazioni nel [portale di Azure](https://portal.azure.com) selezionando il proprio database SQL.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd1c1-177">È anche possibile impostare l'intervallo di aggiornamento e i filtri personalizzati tramite **Abilita opzioni avanzate** dalla finestra di dialogo di connessione.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="dd1c1-178">Dopo avere stabilito la connessione, verrà visualizzato un nuovo set di dati con lo stesso nome del database al cui ci si è connessi.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="dd1c1-179">Selezionare il set di dati per iniziare a progettare un report.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="dd1c1-180">In **Campi** espandere la voce **IISLOGS**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="dd1c1-181">Per creare un report che elenchi le origini URI, selezionare la casella di controllo **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Creazione di un report](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="dd1c1-183">Trascinare quindi **METHOD** nel report.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="dd1c1-184">Il report viene aggiornato per elencare le origini e il metodo HTTP corrispondente usato per la richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![aggiunta dei dati di method](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="dd1c1-186">Nella colonna **Visualizzazioni** selezionare l'icona **Campi** e quindi selezionare la freccia a discesa accanto a **METHOD** nella sezione **Valori**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="dd1c1-187">Per visualizzare il numero di accessi a un URI, selezionare **Conteggio**.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Modifica di un conteggio di method](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="dd1c1-189">Selezionare quindi **Istogramma a colonne in pila** per modificare la modalità di visualizzazione delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Modifica in un grafico in pila](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="dd1c1-191">Per salvare il report, selezionare **Salva** e immettere un nome per il report.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="dd1c1-192">Arrestare la topologia</span><span class="sxs-lookup"><span data-stu-id="dd1c1-192">Stop the topology</span></span>

<span data-ttu-id="dd1c1-193">La topologia rimane in esecuzione fino all'arresto o all'eliminazione del cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="dd1c1-194">Per arrestare la topologia, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="dd1c1-195">In Visual Studio tornare al visualizzatore della topologia e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="dd1c1-196">Fare clic sul pulsante **Termina** per arrestare la topologia.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-196">Select the **Kill** button to stop the topology.</span></span>

    ![Pulsante Termina nel riepilogo della topologia](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="dd1c1-198">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="dd1c1-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="dd1c1-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd1c1-199">Next steps</span></span>

<span data-ttu-id="dd1c1-200">In questo documento è stato illustrato come inviare dati da una topologia Storm al database SQL e quindi visualizzare i dati tramite Power BI.</span><span class="sxs-lookup"><span data-stu-id="dd1c1-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="dd1c1-201">Per informazioni su come usare altre tecnologie di Azure con Storm in HDInsight, vedere il documento seguente:</span><span class="sxs-lookup"><span data-stu-id="dd1c1-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="dd1c1-202">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd1c1-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
