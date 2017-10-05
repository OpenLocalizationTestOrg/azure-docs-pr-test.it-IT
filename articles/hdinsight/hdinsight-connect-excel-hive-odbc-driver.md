---
title: 'Connettere Excel a Hadoop mediante Hive ODBC Driver: Azure HDInsight | Microsoft Docs'
description: Informazioni su come configurare e usare Microsoft Hive ODBC Driver per Excel per eseguire query su dati nei cluster HDInsight da Microsoft Excel.
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="ea165-104">Connettere Excel a Hadoop in HDInsight mediante Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="ea165-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="ea165-105">La soluzione Microsoft per Big Data integra componenti di Microsoft Business Intelligence (BI) con i cluster Apache Hadoop sviluppati da Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea165-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="ea165-106">Un esempio di questa integrazione è la possibilità di connettere Excel al data warehouse Hive di un cluster Hadoop in HDInsight mediante il driver Microsoft Hive Open Database Connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="ea165-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="ea165-107">È inoltre possibile connettere i dati associati a un cluster HDInsight e ad altre origini dati, inclusi altri cluster Hadoop (non HDInsight), da Excel mediante il componente aggiuntivo Microsoft Power Query per Excel.</span><span class="sxs-lookup"><span data-stu-id="ea165-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="ea165-108">Per informazioni sull'installazione e l'uso di Power Query, vedere l'articolo su come [connettere Excel a HDInsight mediante Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="ea165-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="ea165-109">Mentre i passaggi descritti in questo articolo possono essere utilizzati con un cluster HDInsight basato su Windows o Linux, Windows è necessario per la workstation client.</span><span class="sxs-lookup"><span data-stu-id="ea165-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="ea165-110">**Prerequisiti**:</span><span class="sxs-lookup"><span data-stu-id="ea165-110">**Prerequisites**:</span></span>

<span data-ttu-id="ea165-111">Per eseguire le procedure descritte nell'articolo sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea165-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="ea165-112">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ea165-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="ea165-113">Per crearne uno, vedere l'[introduzione ad Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="ea165-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="ea165-114">**Una workstation** con Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="ea165-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="ea165-115">Installare Microsoft Hive ODBC driver</span><span class="sxs-lookup"><span data-stu-id="ea165-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="ea165-116">Scaricare e installare Microsoft Hive ODBC Driver dall'[Area download][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="ea165-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="ea165-117">Questo driver può essere installato nelle versioni a 32 bit o 64 bit di Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="ea165-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="ea165-118">Il driver consente la connessione ad Azure HDInsight (versione 1.6 e successive) e Azure HDInsight Emulator (versione 1.0.0.0 e successive).</span><span class="sxs-lookup"><span data-stu-id="ea165-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="ea165-119">È consigliabile installare la versione corrispondente alla versione dell'applicazione in cui si userà il driver ODBC.</span><span class="sxs-lookup"><span data-stu-id="ea165-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="ea165-120">Per questa esercitazione, il driver verrà usato da Office Excel.</span><span class="sxs-lookup"><span data-stu-id="ea165-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="ea165-121">Creare un'origine dati Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="ea165-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="ea165-122">I passaggi seguenti mostrano come creare un'origine dati Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="ea165-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="ea165-123">In Windows 8 o Windows 10, premere il tasto Windows per aprire la schermata Start e quindi digitare **data sources**.</span><span class="sxs-lookup"><span data-stu-id="ea165-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="ea165-124">Fare clic su **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** a seconda della versione di Office.</span><span class="sxs-lookup"><span data-stu-id="ea165-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="ea165-125">Se si usa Windows 7, scegliere **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** da **Strumenti di amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="ea165-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="ea165-126">Verrà aperta la finestra di dialogo **Amministrazione origine dati ODBC**.</span><span class="sxs-lookup"><span data-stu-id="ea165-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="ea165-127">![Amministrazione origine dati ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurare un DSN usando l'amministrazione origine dati ODBC")</span><span class="sxs-lookup"><span data-stu-id="ea165-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="ea165-128">Nel DNS utente fare clic su **Aggiungi** per aprire la procedura guidata **Crea nuova origine dati**.</span><span class="sxs-lookup"><span data-stu-id="ea165-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="ea165-129">Selezionare **Microsoft Hive ODBC Driver** e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ea165-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="ea165-130">Verrà aperta la finestra di dialogo **Microsoft Hive ODBC Driver DNS Setup** (Configurazione DNS Microsoft Hive ODBC Driver).</span><span class="sxs-lookup"><span data-stu-id="ea165-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="ea165-131">Digitare o selezionare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea165-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="ea165-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ea165-132">Property</span></span> | <span data-ttu-id="ea165-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea165-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ea165-134">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="ea165-134">Data Source Name</span></span> |<span data-ttu-id="ea165-135">Assegnare un nome all'origine dati</span><span class="sxs-lookup"><span data-stu-id="ea165-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="ea165-136">Host</span><span class="sxs-lookup"><span data-stu-id="ea165-136">Host</span></span> |<span data-ttu-id="ea165-137">Immettere &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ea165-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="ea165-138">Ad esempio, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="ea165-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="ea165-139">Porta</span><span class="sxs-lookup"><span data-stu-id="ea165-139">Port</span></span> |<span data-ttu-id="ea165-140">Utilizzare <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="ea165-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="ea165-141">Questa porta è passata da 563 a 443.</span><span class="sxs-lookup"><span data-stu-id="ea165-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="ea165-142">Database</span><span class="sxs-lookup"><span data-stu-id="ea165-142">Database</span></span> |<span data-ttu-id="ea165-143">Usare l'<strong>impostazione predefinita</strong>.</span><span class="sxs-lookup"><span data-stu-id="ea165-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="ea165-144">Mechanism</span><span class="sxs-lookup"><span data-stu-id="ea165-144">Mechanism</span></span> |<span data-ttu-id="ea165-145">Selezionare <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="ea165-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="ea165-146">User Name</span><span class="sxs-lookup"><span data-stu-id="ea165-146">User Name</span></span> |<span data-ttu-id="ea165-147">Immettere il nome utente HTTP del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea165-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="ea165-148">Il nome utente predefinito è <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="ea165-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="ea165-149">Password</span><span class="sxs-lookup"><span data-stu-id="ea165-149">Password</span></span> |<span data-ttu-id="ea165-150">Immettere la password utente del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea165-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="ea165-151">Esistono alcuni importanti parametri a cui prestare attenzione quando si fa clic su **Advanced Options**:</span><span class="sxs-lookup"><span data-stu-id="ea165-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="ea165-152">Parametro</span><span class="sxs-lookup"><span data-stu-id="ea165-152">Parameter</span></span> | <span data-ttu-id="ea165-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea165-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ea165-154">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="ea165-154">Use Native Query</span></span> |<span data-ttu-id="ea165-155">Quando viene selezionato, il driver ODBC NON cerca di convertire TSQL in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ea165-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="ea165-156">Deve essere usato solo se si è assolutamente certi di inviare istruzioni HiveQL pure.</span><span class="sxs-lookup"><span data-stu-id="ea165-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="ea165-157">Quando ci si connette al database SQL Server o SQL di Azure, è consigliabile lasciarlo deselezionato.</span><span class="sxs-lookup"><span data-stu-id="ea165-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="ea165-158">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="ea165-158">Rows fetched per block</span></span> |<span data-ttu-id="ea165-159">Quando si recupera un numero elevato di record, potrebbe essere necessario ottimizzare questo parametro per assicurare prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="ea165-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="ea165-160">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="ea165-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="ea165-161">Le lunghezze e le precisioni del tipo di dati potrebbero avere effetto sulla visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="ea165-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="ea165-162">In questo caso verranno restituite informazioni non corrette a causa della perdita di precisione e/o ai troncamenti.</span><span class="sxs-lookup"><span data-stu-id="ea165-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="ea165-163">![Opzioni avanzate](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opzioni di configurazione DSN avanzate")</span><span class="sxs-lookup"><span data-stu-id="ea165-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="ea165-164">Fare clic su **Test** per testare l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="ea165-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="ea165-165">Quando l'origine dati è configurata correttamente, viene visualizzato *TESTS COMPLETED SUCCESSFULLY!*</span><span class="sxs-lookup"><span data-stu-id="ea165-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="ea165-166">Fare clic su **OK** per chiudere la finestra di dialogo Test.</span><span class="sxs-lookup"><span data-stu-id="ea165-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="ea165-167">La nuova origine dati sarà elencata in **Amministrazione origine dati ODBC**.</span><span class="sxs-lookup"><span data-stu-id="ea165-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="ea165-168">Fare clic su **OK** per chiudere la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="ea165-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="ea165-169">Importazione di dati in Excel da HDInsight</span><span class="sxs-lookup"><span data-stu-id="ea165-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="ea165-170">La procedura seguente descrive come importare dati da una tabella Hive in una cartella di lavoro di Excel usando l'origine dati ODBC creata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ea165-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="ea165-171">Aprire una cartella di lavoro nuova o esistente in Excel.</span><span class="sxs-lookup"><span data-stu-id="ea165-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="ea165-172">Nella scheda **Dati** fare clic su **Dati**, su **Da altre origini** e quindi su **Da ODBC** per avviare **Connessione guidata dati**.</span><span class="sxs-lookup"><span data-stu-id="ea165-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="ea165-173">![Aprire la Connessione guidata dati](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Aprire la Connessione guidata dati")</span><span class="sxs-lookup"><span data-stu-id="ea165-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="ea165-174">Selezione il nome dell'origine dati creata nell'ultima sezione e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea165-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="ea165-175">Immettere il nome utente (il nome predefinito è admin) e la password di Hadoop e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="ea165-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="ea165-176">Nello strumento di spostamento espandere **HIVE** e **default** e quindi fare clic su **hivesampletable** e infine su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="ea165-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="ea165-177">L'importazione dei dati in Excel potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="ea165-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="ea165-178">![Strumento di spostamento per Hive ODBC in HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Aprire Connessione guidata dati")</span><span class="sxs-lookup"><span data-stu-id="ea165-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="ea165-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea165-179">Next steps</span></span>
<span data-ttu-id="ea165-180">In questo articolo è stato illustrato come usare Microsoft Hive ODBC Driver per recuperare dati dal servizio HDInsight in Excel.</span><span class="sxs-lookup"><span data-stu-id="ea165-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="ea165-181">È analogamente possibile recuperare dati dal servizio HDInsight nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="ea165-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="ea165-182">È inoltre possibile caricare dati in un servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea165-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="ea165-183">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="ea165-183">To learn more, see:</span></span>

* <span data-ttu-id="ea165-184">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="ea165-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="ea165-185">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ea165-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ea165-186">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="ea165-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


