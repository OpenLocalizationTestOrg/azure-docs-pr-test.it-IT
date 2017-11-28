---
title: aaaUse Apache Storm con Power BI - HDInsight di Azure | Documenti Microsoft
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="d1afc-103">Utilizzare i dati di Power BI toovisualize da una topologia di Apache Storm</span><span class="sxs-lookup"><span data-stu-id="d1afc-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="d1afc-104">Power BI consente toovisually visualizzare i dati dei report.</span><span class="sxs-lookup"><span data-stu-id="d1afc-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="d1afc-105">Questo documento viene fornito un esempio di come toouse Apache Storm sui dati toogenerate HDInsight per Power BI.</span><span class="sxs-lookup"><span data-stu-id="d1afc-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="d1afc-106">Hello passaggi descritti in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1afc-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="d1afc-107">progetto compilato Hello può essere cluster HDInsight basati su Linux tooa inviato.</span><span class="sxs-lookup"><span data-stu-id="d1afc-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d1afc-108">Solo i cluster basati su Linux creati dopo il 28/10/2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="d1afc-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="d1afc-109">toouse una topologia c# con un cluster basato su Linux, hello aggiornamento pacchetto Microsoft.SCP.Net.SDK NuGet usato dal tooversion progetto 0.10.0.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d1afc-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="d1afc-110">versione di Hello del pacchetto di hello deve corrispondere anche versione principale di hello di Storm installato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1afc-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="d1afc-111">Ad esempio, le versioni 3.3 e 3.4 di Storm in HDInsight usano Storm versione 0.10.x, mentre HDInsight 3.5 usa Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="d1afc-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="d1afc-112">C# topologie nei cluster basati su Linux è necessario utilizzare .NET 4.5 e toorun Mono nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="d1afc-113">Anche se non dovrebbero verificarsi problemi,</span><span class="sxs-lookup"><span data-stu-id="d1afc-113">Most things work.</span></span> <span data-ttu-id="d1afc-114">Tuttavia è necessario controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento per potenziali problemi di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="d1afc-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="d1afc-115">Per una versione Java di questo progetto, che funziona con HDInsight basato su Linux o Windows, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d1afc-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1afc-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d1afc-116">Prerequisites</span></span>

* <span data-ttu-id="d1afc-117">Un utente di Azure Active Directory con accesso [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="d1afc-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="d1afc-118">Un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1afc-118">An HDInsight cluster.</span></span> <span data-ttu-id="d1afc-119">Per altre informazioni, vedere [Introduzione a Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d1afc-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d1afc-120">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d1afc-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d1afc-121">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d1afc-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d1afc-122">Visual Studio (una delle seguenti versioni di hello)</span><span class="sxs-lookup"><span data-stu-id="d1afc-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="d1afc-123">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d1afc-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="d1afc-124">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d1afc-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="d1afc-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d1afc-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="d1afc-126">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="d1afc-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="d1afc-127">Strumenti HDInsight per Visual Studio Hello: vedere [iniziare a usare gli strumenti di HDInsight hello per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) per informazioni sull'installazione delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="d1afc-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d1afc-128">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="d1afc-128">How it works</span></span>

<span data-ttu-id="d1afc-129">Questo esempio contiene una topologia Storm C# che genera in modo casuale i dati di log di Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="d1afc-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="d1afc-130">Questi dati vengono quindi scritti tooa Database SQL, e da qui è usato toogenerate report in Power BI.</span><span class="sxs-lookup"><span data-stu-id="d1afc-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="d1afc-131">Hello file implementare hello funzionalità principale dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d1afc-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="d1afc-132">**SqlAzureBolt.cs**: scrive le informazioni prodotte in hello Storm topologia tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="d1afc-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="d1afc-133">**IISLogsTable.sql**: hello Transact-SQL istruzioni utilizzate toogenerate hello database hello vengono memorizzati in.</span><span class="sxs-lookup"><span data-stu-id="d1afc-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="d1afc-134">Creare la tabella hello in Database SQL prima di avviare topologia hello il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1afc-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="d1afc-135">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="d1afc-135">Download hello example</span></span>

<span data-ttu-id="d1afc-136">Scaricare hello [esempio HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="d1afc-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="d1afc-137">toodownload, una divisione/clone utilizzando [git](http://git-scm.com/), oppure utilizzare hello **scaricare** toodownload collegamento zip dell'archivio di hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="d1afc-138">Creare un database</span><span class="sxs-lookup"><span data-stu-id="d1afc-138">Create a database</span></span>

1. <span data-ttu-id="d1afc-139">toocreate un database, utilizzare i passaggi di hello in hello [esercitazione Database SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="d1afc-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="d1afc-140">Connessione database toohello hello seguente passaggi hello [tooa Database SQL di connettersi con Visual Studio](../sql-database/sql-database-connect-query.md) documento.</span><span class="sxs-lookup"><span data-stu-id="d1afc-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="d1afc-141">In Esplora oggetti, fare doppio clic su database hello e selezionare **nuova Query**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="d1afc-142">Incolla il contenuto di hello di hello **IISLogsTable.sql** i file inclusi in hello scaricato progetto nella finestra query hello e quindi utilizzare Ctrl + Maiusc + query hello tooexecute di E.</span><span class="sxs-lookup"><span data-stu-id="d1afc-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="d1afc-143">Verrà visualizzato un messaggio che hello comandi completati.</span><span class="sxs-lookup"><span data-stu-id="d1afc-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="d1afc-144">Configurare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="d1afc-144">Configure hello sample</span></span>

1. <span data-ttu-id="d1afc-145">Da hello [portale di Azure](https://portal.azure.com), selezionare il database SQL.</span><span class="sxs-lookup"><span data-stu-id="d1afc-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="d1afc-146">Da hello **Essentials** sezione di hello SQL pannello database, seleziona **Mostra le stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="d1afc-147">Elenco hello visualizzato, copiare hello **ADO.NET (autenticazione di SQL)** informazioni.</span><span class="sxs-lookup"><span data-stu-id="d1afc-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="d1afc-148">Aprire l'esempio hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1afc-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="d1afc-149">Da **Esplora**aprire hello **app** file e quindi trovare hello seguente voce:</span><span class="sxs-lookup"><span data-stu-id="d1afc-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="d1afc-150">Sostituire hello **TOBEFILLED # # # #** valore con una stringa di connessione database hello copiato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="d1afc-151">Sostituire **{la\_nome utente}** e **{la\_password}** con hello username e password per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="d1afc-152">Salvare e chiudere il file hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="d1afc-153">Distribuire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="d1afc-153">Deploy hello sample</span></span>

1. <span data-ttu-id="d1afc-154">Da **Esplora**, hello rapida **StormToSQL** del progetto e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d1afc-155">Cluster HDInsight hello selezionare da hello **Cluster Storm** finestra di dialogo elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="d1afc-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d1afc-156">Potrebbe richiedere alcuni secondi per hello **Cluster Storm** toopopulate elenco a discesa con i nomi dei server.</span><span class="sxs-lookup"><span data-stu-id="d1afc-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="d1afc-157">Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1afc-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="d1afc-158">Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1afc-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d1afc-159">Quando è stata inviata la topologia hello, hello __Visualizzatore della topologia__ viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d1afc-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="d1afc-160">tooview questa topologia, la voce SqlAzureWriterTopology hello selezionare dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologie di Hello, con la topologia di hello selezionato](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="d1afc-162">È possibile utilizzare questo toosee Visualizza informazioni sulla topologia di hello o fare doppio clic su un componente di tooa specifico ingresso (ad esempio hello SqlAzureBolt) toosee informazioni nella topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="d1afc-163">Dopo hello topologia è stato eseguito per alcuni minuti, finestra di query SQL toohello restituito è stato utilizzato il database di hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d1afc-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="d1afc-164">Sostituire le istruzioni di hello esistente con hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="d1afc-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="d1afc-165">Utilizzare Ctrl + MAIUSC + E tooexecute hello query e si deve ricevere toohello di risultati simile dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1afc-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="d1afc-166">Questi dati sono state scritte dalla topologia Storm hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="d1afc-167">Creare un report</span><span class="sxs-lookup"><span data-stu-id="d1afc-167">Create a report</span></span>

1. <span data-ttu-id="d1afc-168">Connettersi toohello [connettore Database SQL di Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) per Power BI.</span><span class="sxs-lookup"><span data-stu-id="d1afc-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="d1afc-169">In **Database** selezionare **Recupera**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="d1afc-170">Selezionare **Database SQL di Azure** e quindi **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1afc-171">Potrebbe essere richiesto toodownload hello Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d1afc-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="d1afc-172">In questo caso, utilizzare hello tooconnect i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1afc-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="d1afc-173">Aprire Power BI Desktop e selezionare __Recupera dati__.</span><span class="sxs-lookup"><span data-stu-id="d1afc-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="d1afc-174">2 Selezionare __Azure__ e quindi __Database SQL di Azure__.</span><span class="sxs-lookup"><span data-stu-id="d1afc-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="d1afc-175">Immettere hello informazioni tooconnect tooyour Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1afc-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="d1afc-176">È possibile trovare queste informazioni visitando hello [portale di Azure](https://portal.azure.com) e selezionando il database SQL.</span><span class="sxs-lookup"><span data-stu-id="d1afc-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d1afc-177">È inoltre possibile impostare l'intervallo di aggiornamento hello e filtri personalizzati utilizzando **abilitare opzioni avanzate** da hello finestra di dialogo di connessione.</span><span class="sxs-lookup"><span data-stu-id="d1afc-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="d1afc-178">Dopo aver stabilito la connessione, verrà visualizzato un nuovo set di dati con hello che stesso nome del database hello si è connessi.</span><span class="sxs-lookup"><span data-stu-id="d1afc-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="d1afc-179">Selezionare hello dataset toobegin progettazione di un report.</span><span class="sxs-lookup"><span data-stu-id="d1afc-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="d1afc-180">Da **campi**, espandere hello **IISLOGS** voce.</span><span class="sxs-lookup"><span data-stu-id="d1afc-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="d1afc-181">toocreate deriva un report che elenchi hello URI, selezionare la casella di controllo di hello per **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Creazione di un report](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="d1afc-183">Trascinare quindi **metodo** toohello report.</span><span class="sxs-lookup"><span data-stu-id="d1afc-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="d1afc-184">deriva hello toolist gli aggiornamenti di Hello report e il metodo HTTP corrispondente di hello usata per hello richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1afc-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![aggiunta di dati di hello (metodo)](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="d1afc-186">Da hello **visualizzazioni** colonna, seleziona hello **campi** icona e quindi selezionare hello freccia giù accanto troppo**metodo** in hello **valori**sezione.</span><span class="sxs-lookup"><span data-stu-id="d1afc-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="d1afc-187">Selezionare toodisplay ha avuto un conteggio di quante volte un URI, **conteggio**.</span><span class="sxs-lookup"><span data-stu-id="d1afc-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Modifica il numero di tooa dei metodi](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="d1afc-189">Selezionare quindi hello **istogramma in pila** toochange la modalità di visualizzazione di informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Modifica grafico in pila di tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="d1afc-191">report di hello toosave, selezionare **salvare** e immettere un nome per il report hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d1afc-192">Arrestare la topologia hello</span><span class="sxs-lookup"><span data-stu-id="d1afc-192">Stop hello topology</span></span>

<span data-ttu-id="d1afc-193">topologia Hello continua toorun fino a quando non si arresta o Elimina hello Storm nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1afc-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="d1afc-194">toostop hello topologia, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d1afc-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="d1afc-195">In Visual Studio, restituire toohello Visualizzatore della topologia e selezionare la topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d1afc-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="d1afc-196">Seleziona hello **Kill** topologia di hello toostop pulsante.</span><span class="sxs-lookup"><span data-stu-id="d1afc-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill pulsante sulla topologia di hello riepilogo](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="d1afc-198">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="d1afc-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d1afc-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1afc-199">Next steps</span></span>

<span data-ttu-id="d1afc-200">In questo documento, si è appreso come toosend dati da un tooSQL topologia Storm Database, quindi visualizzare i dati di hello usando Power BI.</span><span class="sxs-lookup"><span data-stu-id="d1afc-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="d1afc-201">Per informazioni su come toowork con altre tecnologie di Azure utilizzando Storm in HDInsight, vedere hello seguente documento:</span><span class="sxs-lookup"><span data-stu-id="d1afc-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="d1afc-202">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1afc-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
