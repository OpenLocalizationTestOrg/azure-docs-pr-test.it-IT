---
title: 'Analizzare i dati di Twitter con Hadoop in HDInsight: Azure | Microsoft Docs'
description: Informazioni su come usare Hive per analizzare i dati di Twitter con Hadoop in HDInsight per rilevare la frequenza d'uso di una parola specifica.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="62c2b-103">Analizzare i dati di Twitter con Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="62c2b-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="62c2b-104">I siti Web di social networking rappresentano una delle principali forze trainanti per l'adozione di Big Data.</span><span class="sxs-lookup"><span data-stu-id="62c2b-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="62c2b-105">Le API pubbliche offerte da siti quali Twitter costituiscono un'utile origine di dati per l'analisi e la comprensione delle tendenze più popolari.</span><span class="sxs-lookup"><span data-stu-id="62c2b-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="62c2b-106">In questa esercitazione si userà l'API di streaming di Twitter per ricevere tweet e quindi si userà Apache Hive in Azure HDInsight per ottenere un elenco di utenti di Twitter che hanno inviato il maggior numero di tweet contenenti una determinata parola.</span><span class="sxs-lookup"><span data-stu-id="62c2b-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62c2b-107">I passaggi descritti in questo documento richiedono un cluster HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="62c2b-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="62c2b-108">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="62c2b-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="62c2b-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="62c2b-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="62c2b-110">Per passaggi specifici di un cluster basato su Linux, vedere [Analizzare i dati di Twitter con Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="62c2b-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62c2b-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="62c2b-111">Prerequisites</span></span>
<span data-ttu-id="62c2b-112">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="62c2b-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="62c2b-113">**Una workstation** in cui sia stato installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c2b-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="62c2b-114">Per eseguire script di Windows PowerShell, è necessario eseguire Azure PowerShell come amministratore e impostare i criteri di esecuzione su *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="62c2b-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="62c2b-115">Vedere [Run Windows PowerShell scripts][powershell-script] (Eseguire script di Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="62c2b-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="62c2b-116">Prima di eseguire script di Windows PowerShell, assicurarsi di essere connessi alla sottoscrizione di Azure usando il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="62c2b-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="62c2b-117">Se si dispone di più sottoscrizioni di Azure, usare il seguente cmdlet per impostare la sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="62c2b-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="62c2b-118">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="62c2b-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="62c2b-119">La procedura descritta in questo documento usa i nuovi cmdlet HDInsight, compatibili con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="62c2b-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="62c2b-120">Per installare la versione più recente, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="62c2b-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="62c2b-121">Se sono presenti script che devono essere modificati per l'uso dei nuovi cmdlet compatibili con Azure Resource Manager, per altre informazioni vedere [Migrazione a strumenti di sviluppo basati su Azure Resource Manager per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="62c2b-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="62c2b-122">**Un cluster HDInsight di Azure**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="62c2b-123">Per istruzioni sul provisioning del cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="62c2b-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="62c2b-124">Il nome del cluster sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="62c2b-125">Nella tabella seguente vengono elencati i file usati nell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="62c2b-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="62c2b-126">File</span><span class="sxs-lookup"><span data-stu-id="62c2b-126">Files</span></span> | <span data-ttu-id="62c2b-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62c2b-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62c2b-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="62c2b-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="62c2b-129">I dati di origine per il processo Hive.</span><span class="sxs-lookup"><span data-stu-id="62c2b-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="62c2b-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="62c2b-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="62c2b-131">Cartella di output per il processo Hive.</span><span class="sxs-lookup"><span data-stu-id="62c2b-131">The output folder for the Hive job.</span></span> <span data-ttu-id="62c2b-132">Il nome file di output del processo Hive relativo al file predefinito è **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="62c2b-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="62c2b-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="62c2b-134">File script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="62c2b-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="62c2b-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="62c2b-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="62c2b-136">Stato del processo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62c2b-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="62c2b-137">Ricezione di feed Twitter</span><span class="sxs-lookup"><span data-stu-id="62c2b-137">Get Twitter feed</span></span>
<span data-ttu-id="62c2b-138">In questa esercitazione verranno usate le [API di streaming di Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="62c2b-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="62c2b-139">L'API di streaming di Twitter specifica che verrà usata è [statuses/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="62c2b-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="62c2b-140">Un file contenente 10.000 tweet e il file di script Hive (descritto nella sezione successiva) sono stati caricati in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="62c2b-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="62c2b-141">Se si preferisce usare i file caricati, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="62c2b-142">[I dati dei tweet](https://dev.twitter.com/docs/platform-objects/tweets) vengono archiviati nel formato JSON (JavaScript Object Notation) che include una struttura annidata complessa.</span><span class="sxs-lookup"><span data-stu-id="62c2b-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="62c2b-143">Invece di scrivere molte righe di codice usando un linguaggio di programmazione convenzionale, è possibile trasformare la struttura annidata in una tabella Hive, in modo da consentire l'esecuzione di query tramite un linguaggio analogo a SQL ( Structured Query Language), denominato HiveQL.</span><span class="sxs-lookup"><span data-stu-id="62c2b-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="62c2b-144">Twitter usa OAuth per fornire accesso autorizzato alla propria API.</span><span class="sxs-lookup"><span data-stu-id="62c2b-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="62c2b-145">OAuth è un protocollo di autenticazione che consente agli utenti di autorizzare l'applicazione ad agire per proprio conto senza divulgare la propria password.</span><span class="sxs-lookup"><span data-stu-id="62c2b-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="62c2b-146">Altre informazioni sono disponibili su [oauth.net](http://oauth.net/) o nell'ottima guida [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) di Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="62c2b-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="62c2b-147">Il primo passaggio da seguire per usare OAuth consiste nel creare una nuova applicazione sul sito Twitter Developers.</span><span class="sxs-lookup"><span data-stu-id="62c2b-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="62c2b-148">**Per creare un'applicazione Twitter**</span><span class="sxs-lookup"><span data-stu-id="62c2b-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="62c2b-149">Accedere a [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="62c2b-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="62c2b-150">Se non si dispone di un account Twitter, fare clic sul collegamento **Sign up now** .</span><span class="sxs-lookup"><span data-stu-id="62c2b-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="62c2b-151">Fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="62c2b-152">Compilare i campi **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="62c2b-153">Per il campo **Website** è possibile creare un URL fittizio.</span><span class="sxs-lookup"><span data-stu-id="62c2b-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="62c2b-154">Nella tabella seguente vengono mostrati alcuni valori di esempio da usare:</span><span class="sxs-lookup"><span data-stu-id="62c2b-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="62c2b-155">Campo</span><span class="sxs-lookup"><span data-stu-id="62c2b-155">Field</span></span> | <span data-ttu-id="62c2b-156">Valore</span><span class="sxs-lookup"><span data-stu-id="62c2b-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="62c2b-157">Nome</span><span class="sxs-lookup"><span data-stu-id="62c2b-157">Name</span></span> |<span data-ttu-id="62c2b-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="62c2b-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="62c2b-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62c2b-159">Description</span></span> |<span data-ttu-id="62c2b-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="62c2b-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="62c2b-161">Website</span><span class="sxs-lookup"><span data-stu-id="62c2b-161">Website</span></span> |<span data-ttu-id="62c2b-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="62c2b-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="62c2b-163">Fare clic su **Yes, I agree** e su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="62c2b-164">Fare clic sulla scheda **Permissions** .</span><span class="sxs-lookup"><span data-stu-id="62c2b-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="62c2b-165">L'autorizzazione predefinita è **Read only**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-165">The default permission is **Read only**.</span></span> <span data-ttu-id="62c2b-166">Questo livello di autorizzazione è sufficiente per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="62c2b-167">Fare clic sulla scheda **Keys and Access Tokens** .</span><span class="sxs-lookup"><span data-stu-id="62c2b-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="62c2b-168">Fare clic su **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="62c2b-169">Fare clic su **Test OAuth** nell'angolo superiore destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="62c2b-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="62c2b-170">Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="62c2b-171">Sarà necessario usare questi valori più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="62c2b-172">In questa esercitazione si userà Windows PowerShell per effettuare la chiamata del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="62c2b-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="62c2b-173">Per un esempio di .NET C#, vedere [Analizzare i sentiment di Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="62c2b-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="62c2b-174">L'altro strumento di ampia diffusione per effettuare chiamate di servizi Web è [*Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="62c2b-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="62c2b-175">Curl può essere scaricato da [questa pagina][curl-download].</span><span class="sxs-lookup"><span data-stu-id="62c2b-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="62c2b-176">Quando si usa il comando curl in Windows, per i valori delle opzioni usare le virgolette doppie invece di quelle singole.</span><span class="sxs-lookup"><span data-stu-id="62c2b-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="62c2b-177">**Per ricevere tweet**</span><span class="sxs-lookup"><span data-stu-id="62c2b-177">**To get tweets**</span></span>

1. <span data-ttu-id="62c2b-178">Aprire Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="62c2b-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="62c2b-179">Nella schermata Start di Windows 8 digitare **PowerShell_ISE** e quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="62c2b-180">Vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="62c2b-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="62c2b-181">Copiare lo script seguente nel riquadro di script:</span><span class="sxs-lookup"><span data-stu-id="62c2b-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="62c2b-182">Impostare le prime cinque-otto variabili dello script:</span><span class="sxs-lookup"><span data-stu-id="62c2b-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="62c2b-183">Variabile</span><span class="sxs-lookup"><span data-stu-id="62c2b-183">Variable</span></span>|<span data-ttu-id="62c2b-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62c2b-184">Description</span></span>
    ---|---
    <span data-ttu-id="62c2b-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="62c2b-185">$clusterName</span></span>|<span data-ttu-id="62c2b-186">Nome del cluster HDInsight in cui eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="62c2b-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="62c2b-187">$oauth_consumer_key</span></span>|<span data-ttu-id="62c2b-188">Applicazione Twitter **consumer key** scritta in precedenza al momento della creazione dell'applicazione Twitter.</span><span class="sxs-lookup"><span data-stu-id="62c2b-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="62c2b-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="62c2b-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="62c2b-190">L'applicazione Twitter **consumer secret** scritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c2b-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="62c2b-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="62c2b-191">$oauth_token</span></span>|<span data-ttu-id="62c2b-192">L'applicazione Twitter **access token** scritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c2b-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="62c2b-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="62c2b-193">$oauth_token_secret</span></span>|<span data-ttu-id="62c2b-194">L'applicazione Twitter **access token secret** scritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c2b-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="62c2b-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="62c2b-195">$destBlobName</span></span>|<span data-ttu-id="62c2b-196">Il nome BLOB dell'output.</span><span class="sxs-lookup"><span data-stu-id="62c2b-196">This is the output blob name.</span></span> <span data-ttu-id="62c2b-197">Il valore predefinito è **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="62c2b-198">Se si modifica il valore predefinito, sarà necessario aggiornare gli script di Windows PowerShell di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="62c2b-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="62c2b-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="62c2b-199">$trackString</span></span>|<span data-ttu-id="62c2b-200">Il servizio Web restituirà tweet correlati a queste parole chiave.</span><span class="sxs-lookup"><span data-stu-id="62c2b-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="62c2b-201">Il valore predefinito è **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="62c2b-202">Se si modifica il valore predefinito, si dovranno aggiornare gli script di Windows PowerShell di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="62c2b-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="62c2b-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="62c2b-203">$lineMax</span></span>|<span data-ttu-id="62c2b-204">Il valore determina il numero di tweet che lo script leggerà.</span><span class="sxs-lookup"><span data-stu-id="62c2b-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="62c2b-205">Per leggere 100 tweet sono necessari circa tre minuti.</span><span class="sxs-lookup"><span data-stu-id="62c2b-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="62c2b-206">È possibile impostare un numero più elevato, ma il download richiederà più tempo.</span><span class="sxs-lookup"><span data-stu-id="62c2b-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="62c2b-207">Premere **F5** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="62c2b-207">Press **F5** to run the script.</span></span> <span data-ttu-id="62c2b-208">In caso di problemi, come soluzione selezionare tutte le righe e premere **F8**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="62c2b-209">Alla fine dell'output verrà visualizzato</span><span class="sxs-lookup"><span data-stu-id="62c2b-209">You shall see "Complete!"</span></span> <span data-ttu-id="62c2b-210">"Completato".</span><span class="sxs-lookup"><span data-stu-id="62c2b-210">at the end of the output.</span></span> <span data-ttu-id="62c2b-211">Eventuali messaggi di errore verranno visualizzati in rosso.</span><span class="sxs-lookup"><span data-stu-id="62c2b-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="62c2b-212">Come procedura di convalida, è possibile controllare il file di output, **/tutorials/twitter/data/tweets.txt**, nell'archivio BLOB di Azure tramite uno strumento per l'esplorazione dei servizi di archiviazione di Azure oppure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c2b-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="62c2b-213">Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="62c2b-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="62c2b-214">Creare uno script HiveQL</span><span class="sxs-lookup"><span data-stu-id="62c2b-214">Create HiveQL script</span></span>
<span data-ttu-id="62c2b-215">Azure PowerShell consente di eseguire più istruzioni HiveQL contemporaneamente o di inserire l'istruzione HiveQL in un file di script.</span><span class="sxs-lookup"><span data-stu-id="62c2b-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="62c2b-216">In questa esercitazione verrà creato uno script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="62c2b-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="62c2b-217">Il file di script deve essere caricato nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="62c2b-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="62c2b-218">Nella sezione successiva si eseguirà il file di script tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c2b-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="62c2b-219">Il file di script Hive e un file contenente 10.000 tweet sono stati caricati in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="62c2b-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="62c2b-220">Se si preferisce usare i file caricati, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="62c2b-221">Il file di script HiveQL eseguirà le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62c2b-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="62c2b-222">**Eliminazione della tabella tweets_raw** nel caso in cui la tabella esista già.</span><span class="sxs-lookup"><span data-stu-id="62c2b-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="62c2b-223">**Creazione della tabella tweets_raw Hive**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="62c2b-224">Questa tabella Hive strutturata e temporanea contiene i dati per altri processi di estrazione, trasformazione e caricamento (ETL, Extraction, Transformation, and Loading).</span><span class="sxs-lookup"><span data-stu-id="62c2b-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="62c2b-225">Per informazioni sulle partizioni, vedere [Hive tutorial][apache-hive-tutorial] (Esercitazione su Hive).</span><span class="sxs-lookup"><span data-stu-id="62c2b-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="62c2b-226">**Caricare i dati** dalla cartella di origine /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="62c2b-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="62c2b-227">Il set di dati di tweet di grandi dimensioni in formato JSON annidato è stato trasformato in una struttura di tabella Hive temporanea.</span><span class="sxs-lookup"><span data-stu-id="62c2b-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="62c2b-228">**Eliminare la tabella tweets** nel caso esista già.</span><span class="sxs-lookup"><span data-stu-id="62c2b-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="62c2b-229">**Creare la tabella tweets**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-229">**Create the tweets table**.</span></span> <span data-ttu-id="62c2b-230">Prima di eseguire query sul set di dati di tweet tramite Hive, è necessario eseguire un altro processo ETL.</span><span class="sxs-lookup"><span data-stu-id="62c2b-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="62c2b-231">Il processo ETL definisce uno schema di tabella più dettagliato per i dati archiviati nella tabella "twitter_raw".</span><span class="sxs-lookup"><span data-stu-id="62c2b-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="62c2b-232">**Inserire la tabella di sovrascrittura**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-232">**Insert overwrite table**.</span></span> <span data-ttu-id="62c2b-233">Questo script Hive complesso avvia una serie di processi MapReduce dal cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62c2b-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="62c2b-234">In base al set di dati e alla dimensione del cluster, tale operazione potrebbe richiedere circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="62c2b-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="62c2b-235">**Inserire la directory di sovrascrittura**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="62c2b-236">Eseguire una query e inviare il set di dati a un file.</span><span class="sxs-lookup"><span data-stu-id="62c2b-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="62c2b-237">Questa query restituirà un elenco di utenti di Twitter che hanno inviato il maggior numero di tweet contenenti la parola "Azure".</span><span class="sxs-lookup"><span data-stu-id="62c2b-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="62c2b-238">**Per creare uno script Hive e caricarlo in Azure**</span><span class="sxs-lookup"><span data-stu-id="62c2b-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="62c2b-239">Aprire Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="62c2b-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="62c2b-240">Copiare lo script seguente nel riquadro di script:</span><span class="sxs-lookup"><span data-stu-id="62c2b-240">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="62c2b-241">Impostare le prime due variabili nello script:</span><span class="sxs-lookup"><span data-stu-id="62c2b-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="62c2b-242">Variabile</span><span class="sxs-lookup"><span data-stu-id="62c2b-242">Variable</span></span> | <span data-ttu-id="62c2b-243">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62c2b-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="62c2b-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="62c2b-244">$clusterName</span></span> |<span data-ttu-id="62c2b-245">Immettere il nome del cluster HDInsight in cui eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="62c2b-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="62c2b-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="62c2b-246">$subscriptionID</span></span> |<span data-ttu-id="62c2b-247">Inserire L'ID della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="62c2b-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="62c2b-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="62c2b-248">$sourceDataPath</span></span> |<span data-ttu-id="62c2b-249">Percorso dell'archivio BLOB di Azure dal quale le query Hive leggeranno i dati.</span><span class="sxs-lookup"><span data-stu-id="62c2b-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="62c2b-250">Non è necessario modificare questa variabile.</span><span class="sxs-lookup"><span data-stu-id="62c2b-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="62c2b-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="62c2b-251">$outputPath</span></span> |<span data-ttu-id="62c2b-252">Percorso dell'archivio BLOB di Azure dal quale le query Hive restituiranno i risultati.</span><span class="sxs-lookup"><span data-stu-id="62c2b-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="62c2b-253">Non è necessario modificare questa variabile.</span><span class="sxs-lookup"><span data-stu-id="62c2b-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="62c2b-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="62c2b-254">$hqlScriptFile</span></span> |<span data-ttu-id="62c2b-255">Posizione e nome del file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="62c2b-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="62c2b-256">Non è necessario modificare questa variabile.</span><span class="sxs-lookup"><span data-stu-id="62c2b-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="62c2b-257">Premere **F5** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="62c2b-257">Press **F5** to run the script.</span></span> <span data-ttu-id="62c2b-258">In caso di problemi, come soluzione selezionare tutte le righe e premere **F8**.</span><span class="sxs-lookup"><span data-stu-id="62c2b-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="62c2b-259">Alla fine dell'output verrà visualizzato</span><span class="sxs-lookup"><span data-stu-id="62c2b-259">You shall see "Complete!"</span></span> <span data-ttu-id="62c2b-260">"Completato".</span><span class="sxs-lookup"><span data-stu-id="62c2b-260">at the end of the output.</span></span> <span data-ttu-id="62c2b-261">Eventuali messaggi di errore verranno visualizzati in rosso.</span><span class="sxs-lookup"><span data-stu-id="62c2b-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="62c2b-262">Come procedura di convalida, è possibile controllare il file di output, **/tutorials/twitter/twitter.hql**, nell'archivio BLOB di Azure usando uno strumento per l'esplorazione dei servizi di archiviazione Azure oppure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c2b-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="62c2b-263">Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="62c2b-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="62c2b-264">Elaborare i dati di Twitter tramite Hive</span><span class="sxs-lookup"><span data-stu-id="62c2b-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="62c2b-265">Tutte le attività preliminari sono state completate.</span><span class="sxs-lookup"><span data-stu-id="62c2b-265">You have finished all the preparation work.</span></span> <span data-ttu-id="62c2b-266">Ora è possibile richiamare lo script Hive script e controllare i risultati.</span><span class="sxs-lookup"><span data-stu-id="62c2b-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="62c2b-267">Inviare un processo Hive</span><span class="sxs-lookup"><span data-stu-id="62c2b-267">Submit a Hive job</span></span>
<span data-ttu-id="62c2b-268">Usare lo script PowerShell seguente per eseguire lo script Hive.</span><span class="sxs-lookup"><span data-stu-id="62c2b-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="62c2b-269">È necessario impostare la prima variabile.</span><span class="sxs-lookup"><span data-stu-id="62c2b-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="62c2b-270">Per usare i tweet e lo script HiveQL caricati nelle ultime due sezioni, impostare $hqlScriptFile su "/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="62c2b-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="62c2b-271">Per usare quelli caricati in un BLOB pubblico per l'utente, impostare $hqlScriptFile su "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="62c2b-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="62c2b-272">Controllare i risultati</span><span class="sxs-lookup"><span data-stu-id="62c2b-272">Check the results</span></span>
<span data-ttu-id="62c2b-273">Usare lo script di Windows PowerShell seguente per controllare l'output del processo Hive.</span><span class="sxs-lookup"><span data-stu-id="62c2b-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="62c2b-274">È necessario impostare le prime due variabili.</span><span class="sxs-lookup"><span data-stu-id="62c2b-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> La tabella Hive usa \001 come delimitatore di campo. <span data-ttu-id="62c2b-276">Il delimitatore non è visibile nell'output.</span><span class="sxs-lookup"><span data-stu-id="62c2b-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="62c2b-277">Dopo che i risultati dell'analisi sono stati inserivi in un archivio BLOB di Azure, è possibile esportare i dati in un database SQL o un server SQL di Azure, esportare i dati in Excel tramite Power Query oppure connettere l'applicazione ai dati usando Hive ODBC Driver.</span><span class="sxs-lookup"><span data-stu-id="62c2b-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="62c2b-278">Per altre informazioni, vedere [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop], [Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-delay-data], [Connettere Excel a HDInsight mediante Power Query][hdinsight-power-query] e [Connettere Excel a HDInsight mediante Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="62c2b-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="62c2b-279">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62c2b-279">Next steps</span></span>
<span data-ttu-id="62c2b-280">In questa esercitazione è stato illustrato come trasformare un set di dati JSON non strutturato in una tabella Hive strutturata per eseguire query, esplorare e analizzare dati da Twitter tramite HDInsight in Azure.</span><span class="sxs-lookup"><span data-stu-id="62c2b-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="62c2b-281">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="62c2b-281">To learn more, see:</span></span>

* <span data-ttu-id="62c2b-282">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="62c2b-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="62c2b-283">[Analizzare i sentimenti Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="62c2b-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="62c2b-284">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="62c2b-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="62c2b-285">[Connettere Excel a HDInsight mediante Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="62c2b-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="62c2b-286">[Connettere Excel a HDInsight mediante Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="62c2b-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="62c2b-287">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="62c2b-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
