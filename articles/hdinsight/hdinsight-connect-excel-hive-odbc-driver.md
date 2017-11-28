---
title: aaaConnect tooHadoop di Excel con hello Hive Driver ODBC - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come tooset backup e utilizzare hello Hive driver ODBC Microsoft per i dati di Excel tooquery nel cluster HDInsight da Microsoft Excel.
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="d6cbb-104">Connettere Excel tooHadoop in Azure HDInsight con hello Hive di Microsoft ODBC driver</span><span class="sxs-lookup"><span data-stu-id="d6cbb-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="d6cbb-105">Soluzione Big Data Microsoft integra i componenti di Microsoft Business Intelligence (BI) con i cluster Apache Hadoop che sono stati distribuiti da hello Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="d6cbb-106">Un esempio di tale integrazione è hello possibilità tooconnect Excel toohello Hive del data warehouse di un cluster Hadoop in HDInsight mediante hello Driver Microsoft Hive Open Database Connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="d6cbb-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="d6cbb-107">È inoltre possibile tooconnect dati di hello associati a un cluster HDInsight e altre origini dati, inclusi altri (non-HDInsight) Hadoop cluster, da Excel utilizzando hello componente aggiuntivo di Microsoft Power Query per Excel.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="d6cbb-108">Per informazioni sull'installazione e utilizzo di Power Query, vedere [tooHDInsight Excel connettersi con Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="d6cbb-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="d6cbb-109">Mentre hello i passaggi questo articolo può essere utilizzato con uno Linux o cluster HDInsight basati su Windows, Windows è richiesto per workstation client hello.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="d6cbb-110">**Prerequisiti**:</span><span class="sxs-lookup"><span data-stu-id="d6cbb-110">**Prerequisites**:</span></span>

<span data-ttu-id="d6cbb-111">Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d6cbb-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="d6cbb-112">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="d6cbb-113">toocreate uno, vedere [Guida introduttiva di Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="d6cbb-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="d6cbb-114">**Una workstation** con Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="d6cbb-115">Installare Microsoft Hive ODBC driver</span><span class="sxs-lookup"><span data-stu-id="d6cbb-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="d6cbb-116">Scaricare e installare il Driver Microsoft ODBC Hive dal hello [area Download][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="d6cbb-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="d6cbb-117">Questo driver può essere installato nelle versioni a 32 bit o 64 bit di Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="d6cbb-118">driver Hello consente tooAzure connessione HDInsight (versione 1.6 e versioni successive) e l'emulatore di Azure HDInsight (v.1.0.0.0 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="d6cbb-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="d6cbb-119">Installare versione hello corrispondente versione di hello di un'applicazione hello in cui si usa il driver ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="d6cbb-120">Per questa esercitazione, il driver hello viene utilizzato da Office Excel.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="d6cbb-121">Creare un'origine dati Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="d6cbb-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="d6cbb-122">Hello passaggi seguenti viene illustrato come toocreate un Hive origine dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="d6cbb-123">In Windows 8 o Windows 10, premere la schermata iniziale hello Windows tooopen chiave hello e quindi digitare **origini dati**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="d6cbb-124">Fare clic su **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** a seconda della versione di Office.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="d6cbb-125">Se si usa Windows 7, scegliere **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** da **Strumenti di amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="d6cbb-126">Verrà visualizzato hello **Amministrazione origine dati ODBC** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="d6cbb-127">![Amministrazione origine dati ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurare un DSN usando l'amministrazione origine dati ODBC")</span><span class="sxs-lookup"><span data-stu-id="d6cbb-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="d6cbb-128">Da utente DNS, fare clic su **Aggiungi** tooopen hello **Crea nuova origine dati** procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="d6cbb-129">Selezionare **Microsoft Hive ODBC Driver** e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="d6cbb-130">Verrà visualizzato hello **Hive ODBC Driver DNS installazione di Microsoft** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="d6cbb-131">Digitare o selezionare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="d6cbb-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="d6cbb-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d6cbb-132">Property</span></span> | <span data-ttu-id="d6cbb-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6cbb-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="d6cbb-134">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="d6cbb-134">Data Source Name</span></span> |<span data-ttu-id="d6cbb-135">Fornire un'origine dati di nome tooyour</span><span class="sxs-lookup"><span data-stu-id="d6cbb-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="d6cbb-136">Host</span><span class="sxs-lookup"><span data-stu-id="d6cbb-136">Host</span></span> |<span data-ttu-id="d6cbb-137">Immettere &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="d6cbb-138">Ad esempio, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="d6cbb-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="d6cbb-139">Porta</span><span class="sxs-lookup"><span data-stu-id="d6cbb-139">Port</span></span> |<span data-ttu-id="d6cbb-140">Utilizzare <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="d6cbb-141">(Questa porta è stata modificata da too443 563).</span><span class="sxs-lookup"><span data-stu-id="d6cbb-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="d6cbb-142">Database</span><span class="sxs-lookup"><span data-stu-id="d6cbb-142">Database</span></span> |<span data-ttu-id="d6cbb-143">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="d6cbb-144">Mechanism</span><span class="sxs-lookup"><span data-stu-id="d6cbb-144">Mechanism</span></span> |<span data-ttu-id="d6cbb-145">Selezionare <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="d6cbb-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="d6cbb-146">User Name</span><span class="sxs-lookup"><span data-stu-id="d6cbb-146">User Name</span></span> |<span data-ttu-id="d6cbb-147">Immettere il nome utente HTTP del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="d6cbb-148">nome utente predefinito Hello <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="d6cbb-149">Password</span><span class="sxs-lookup"><span data-stu-id="d6cbb-149">Password</span></span> |<span data-ttu-id="d6cbb-150">Immettere la password utente del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="d6cbb-151">Esistono alcuni toobe importanti parametri conoscere quando fa clic su **opzioni avanzate**:</span><span class="sxs-lookup"><span data-stu-id="d6cbb-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="d6cbb-152">.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-152">Parameter</span></span> | <span data-ttu-id="d6cbb-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6cbb-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="d6cbb-154">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="d6cbb-154">Use Native Query</span></span> |<span data-ttu-id="d6cbb-155">Quando è selezionata, il driver ODBC di hello non tenta tooconvert TSQL in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="d6cbb-156">Deve essere usato solo se si è assolutamente certi di inviare istruzioni HiveQL pure.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="d6cbb-157">Quando ci si connette tooSQL Server o Database SQL di Azure, è necessario lasciarla deselezionata.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="d6cbb-158">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="d6cbb-158">Rows fetched per block</span></span> |<span data-ttu-id="d6cbb-159">Durante il recupero di un numero elevato di record, l'ottimizzazione di questo parametro può essere prestazioni ottimali tooensure obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="d6cbb-160">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="d6cbb-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="d6cbb-161">lunghezza del tipo di dati Hello e precisione possono influire sulle modalità di restituzione di dati.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="d6cbb-162">Provocano toobe informazioni non corrette restituite scadenza tooloss di precisione e/o il troncamento.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="d6cbb-163">![Opzioni avanzate](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opzioni di configurazione DSN avanzate")</span><span class="sxs-lookup"><span data-stu-id="d6cbb-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="d6cbb-164">Fare clic su **Test** origine dati di tootest hello.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="d6cbb-165">Quando l'origine dati hello è configurata correttamente, viene visualizzato *verifica completata!*.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="d6cbb-166">Fare clic su **OK** finestra di dialogo tooclose hello Test.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="d6cbb-167">nuova origine dei dati Hello è elencati in hello **Amministrazione origine dati ODBC**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="d6cbb-168">Fare clic su **OK** guidata hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="d6cbb-169">Importazione di dati in Excel da HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6cbb-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="d6cbb-170">Hello passaggi seguenti descrivono hello modo tooimport dati da una tabella Hive in una cartella di lavoro di Excel utilizzando l'origine di dati ODBC hello creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="d6cbb-171">Aprire una cartella di lavoro nuova o esistente in Excel.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="d6cbb-172">Da hello **dati** scheda, fare clic su **recupera dati**, fare clic su **da altre origini**, quindi fare clic su **da ODBC** toolaunch hello  **Connessione guidata dati**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="d6cbb-173">![Aprire la Connessione guidata dati](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Aprire la Connessione guidata dati")</span><span class="sxs-lookup"><span data-stu-id="d6cbb-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="d6cbb-174">Nome creato nell'ultima sezione hello dell'origine dati selezionare hello e quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="d6cbb-175">Immettere nome utente di Hadoop (nome predefinito hello è admin) hello password e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="d6cbb-176">Nello strumento di spostamento espandere **HIVE** e **default** e quindi fare clic su **hivesampletable** e infine su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="d6cbb-177">Alcuni secondi prima del recupero dei dati importati tooExcel necessario.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="d6cbb-178">![Strumento di spostamento per Hive ODBC in HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Aprire Connessione guidata dati")</span><span class="sxs-lookup"><span data-stu-id="d6cbb-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6cbb-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6cbb-179">Next steps</span></span>
<span data-ttu-id="d6cbb-180">In questo articolo è stato descritto come toouse hello dati tooretrieve del driver ODBC di Microsoft Hive da hello HDInsight Service in Excel.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="d6cbb-181">Analogamente, è possibile recuperare dati da hello HDInsight Service nel Database SQL.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="d6cbb-182">È inoltre dati tooupload possibili in un HDInsight Service.</span><span class="sxs-lookup"><span data-stu-id="d6cbb-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="d6cbb-183">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="d6cbb-183">toolearn more, see:</span></span>

* <span data-ttu-id="d6cbb-184">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="d6cbb-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="d6cbb-185">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d6cbb-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d6cbb-186">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="d6cbb-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


