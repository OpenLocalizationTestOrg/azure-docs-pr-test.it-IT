---
title: dati di Twitter con Hadoop in HDInsight - Azure aaaAnalyze | Documenti Microsoft
description: Informazioni su come toouse Hive tooanalyze Twitter dei dati in Hadoop in HDInsight toofind hello frequenza di utilizzo di una determinata parola.
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
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="bd938-103">Analizzare i dati di Twitter con Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd938-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="bd938-104">Siti Web sociali sono uno dei hello principali le forze per l'adozione dei big data.</span><span class="sxs-lookup"><span data-stu-id="bd938-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="bd938-105">Le API pubbliche offerte da siti quali Twitter costituiscono un'utile origine di dati per l'analisi e la comprensione delle tendenze più popolari.</span><span class="sxs-lookup"><span data-stu-id="bd938-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="bd938-106">In questa esercitazione consente di ottenere TWEET utilizzando un Twitter streaming API e di utilizzare Apache Hive in Azure HDInsight tooget un elenco di utenti di Twitter che ha inviato hello TWEET la maggior parte dei contenuti di una determinata parola.</span><span class="sxs-lookup"><span data-stu-id="bd938-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd938-107">Hello passaggi in questo documento richiedono un cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="bd938-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="bd938-108">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="bd938-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bd938-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bd938-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="bd938-110">Per cluster basati su Linux tooa specifica di passaggi, vedere [dati analizzare Twitter usando Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bd938-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd938-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd938-111">Prerequisites</span></span>
<span data-ttu-id="bd938-112">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="bd938-113">**Una workstation** in cui sia stato installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd938-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="bd938-114">script di Windows PowerShell tooexecute, è necessario eseguire Azure PowerShell come amministratore e impostare i criteri di esecuzione hello troppo*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="bd938-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="bd938-115">Vedere [Run Windows PowerShell scripts][powershell-script] (Eseguire script di Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="bd938-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="bd938-116">Prima di eseguire script di Windows PowerShell, verificare di disporre connesso tooyour sottoscrizione di Azure tramite hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd938-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="bd938-117">Se si dispone di più sottoscrizioni di Azure, utilizzare hello sottoscrizione corrente hello tooset di cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd938-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="bd938-118">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="bd938-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="bd938-119">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd938-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="bd938-120">Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd938-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="bd938-121">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="bd938-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="bd938-122">**Un cluster HDInsight di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bd938-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="bd938-123">Per istruzioni sul provisioning del cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="bd938-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="bd938-124">Nome del cluster hello sarà necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="bd938-125">Hello nella tabella seguente sono elencati i file hello utilizzati in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="bd938-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="bd938-126">File</span><span class="sxs-lookup"><span data-stu-id="bd938-126">Files</span></span> | <span data-ttu-id="bd938-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bd938-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd938-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="bd938-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="bd938-129">dati di origine Hello per processo Hive hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="bd938-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="bd938-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="bd938-131">cartella di output di Hello per processo Hive hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="bd938-132">Hello Hive processo output nome file predefinito è **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="bd938-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="bd938-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="bd938-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="bd938-134">file di script HiveQL Hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="bd938-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="bd938-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="bd938-136">lo stato del processo Hadoop Hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="bd938-137">Ricezione di feed Twitter</span><span class="sxs-lookup"><span data-stu-id="bd938-137">Get Twitter feed</span></span>
<span data-ttu-id="bd938-138">In questa esercitazione si utilizzerà hello [Twitter API di flusso][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="bd938-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="bd938-139">è Hello Twitter specifico streaming API si utilizzerà [stati/filtro][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="bd938-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="bd938-140">Un file contenente 10.000 TWEET e file di script Hive hello (descritta nella sezione successiva hello) sono stati caricati in un contenitore di Blob pubblico.</span><span class="sxs-lookup"><span data-stu-id="bd938-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="bd938-141">È possibile ignorare questa sezione se si desidera toouse hello caricamento file.</span><span class="sxs-lookup"><span data-stu-id="bd938-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="bd938-142">[TWEET dati](https://dev.twitter.com/docs/platform-objects/tweets) viene archiviato in formato JavaScript Object Notation (JSON) hello che contiene una struttura nidificata complessa.</span><span class="sxs-lookup"><span data-stu-id="bd938-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="bd938-143">Invece di scrivere molte righe di codice usando un linguaggio di programmazione convenzionale, è possibile trasformare la struttura annidata in una tabella Hive, in modo da consentire l'esecuzione di query tramite un linguaggio analogo a SQL ( Structured Query Language), denominato HiveQL.</span><span class="sxs-lookup"><span data-stu-id="bd938-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="bd938-144">Twitter utilizza OAuth tooprovide autorizzato accesso tooits API.</span><span class="sxs-lookup"><span data-stu-id="bd938-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="bd938-145">OAuth è un protocollo di autenticazione che consente agli utenti tooapprove applicazioni tooact per conto del cliente senza condividere la propria password.</span><span class="sxs-lookup"><span data-stu-id="bd938-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="bd938-146">Altre informazioni sono reperibile in [oauth.net](http://oauth.net/) o hello eccellente [tooOAuth Guida per principianti](http://hueniverse.com/oauth/) da Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="bd938-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="bd938-147">Hello primo passaggio toouse OAuth è toocreate una nuova applicazione nel sito per sviluppatori di Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="bd938-148">**toocreate un'applicazione di Twitter**</span><span class="sxs-lookup"><span data-stu-id="bd938-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="bd938-149">Accedi troppo[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="bd938-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="bd938-150">Fare clic su hello **Iscriviti ora** collegare se non si dispone di un account Twitter.</span><span class="sxs-lookup"><span data-stu-id="bd938-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="bd938-151">Fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="bd938-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="bd938-152">Compilare i campi **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="bd938-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="bd938-153">Si può creare un URL per hello **sito Web** campo.</span><span class="sxs-lookup"><span data-stu-id="bd938-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="bd938-154">Hello nella tabella seguente mostra alcuni toouse di valori di esempio:</span><span class="sxs-lookup"><span data-stu-id="bd938-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="bd938-155">Campo</span><span class="sxs-lookup"><span data-stu-id="bd938-155">Field</span></span> | <span data-ttu-id="bd938-156">Valore</span><span class="sxs-lookup"><span data-stu-id="bd938-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="bd938-157">Nome</span><span class="sxs-lookup"><span data-stu-id="bd938-157">Name</span></span> |<span data-ttu-id="bd938-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="bd938-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="bd938-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bd938-159">Description</span></span> |<span data-ttu-id="bd938-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="bd938-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="bd938-161">Website</span><span class="sxs-lookup"><span data-stu-id="bd938-161">Website</span></span> |<span data-ttu-id="bd938-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="bd938-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="bd938-163">Fare clic su **Yes, I agree** e su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="bd938-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="bd938-164">Fare clic su hello **autorizzazioni** all'autorizzazione predefinita hello scheda **di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="bd938-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="bd938-165">Questo livello di autorizzazione è sufficiente per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bd938-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="bd938-166">Fare clic su hello **chiavi e i token di accesso** scheda.</span><span class="sxs-lookup"><span data-stu-id="bd938-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="bd938-167">Fare clic su **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="bd938-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="bd938-168">Fare clic su **Test OAuth** nell'angolo superiore destro di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="bd938-169">Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="bd938-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="bd938-170">I valori hello sarà necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="bd938-171">In questa esercitazione si utilizzerà chiamata del servizio web di Windows PowerShell toomake hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="bd938-172">Per un esempio di .NET C#, vedere [Analizzare i sentiment di Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="bd938-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="bd938-173">è Hello altre chiamate al servizio web toomake strumento comune [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="bd938-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="bd938-174">Curl può essere scaricato da [questa pagina][curl-download].</span><span class="sxs-lookup"><span data-stu-id="bd938-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="bd938-175">Quando si utilizza il comando di curl hello in Windows, utilizzare le virgolette doppie anziché le virgolette singole per i valori di opzione hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="bd938-176">**tooget tweets**</span><span class="sxs-lookup"><span data-stu-id="bd938-176">**tooget tweets**</span></span>

1. <span data-ttu-id="bd938-177">Aprire Windows PowerShell Integrated Scripting Environment (ISE) hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="bd938-178">(Nella schermata iniziale di Windows 8 hello digitare **PowerShell_ISE** e quindi fare clic su **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="bd938-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="bd938-179">Vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).</span><span class="sxs-lookup"><span data-stu-id="bd938-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="bd938-180">Copiare lo script seguente nel riquadro di script hello hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="bd938-181">Impostare le variabili tooeight primi cinque hello nello script hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="bd938-182">Variabile</span><span class="sxs-lookup"><span data-stu-id="bd938-182">Variable</span></span>|<span data-ttu-id="bd938-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bd938-183">Description</span></span>
    ---|---
    <span data-ttu-id="bd938-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="bd938-184">$clusterName</span></span>|<span data-ttu-id="bd938-185">Questo è il nome di hello del cluster HDInsight hello in cui si desidera un'applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="bd938-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="bd938-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="bd938-186">$oauth_consumer_key</span></span>|<span data-ttu-id="bd938-187">Si tratta di un'applicazione hello Twitter **chiave consumer** annotato in precedenza durante la creazione di un'applicazione hello Twitter.</span><span class="sxs-lookup"><span data-stu-id="bd938-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="bd938-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="bd938-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="bd938-189">Si tratta di un'applicazione hello Twitter **segreto del cliente** annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd938-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="bd938-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="bd938-190">$oauth_token</span></span>|<span data-ttu-id="bd938-191">Si tratta di un'applicazione hello Twitter **token di accesso** annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd938-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="bd938-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="bd938-192">$oauth_token_secret</span></span>|<span data-ttu-id="bd938-193">Si tratta di un'applicazione hello Twitter **segreto del token di accesso** annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd938-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="bd938-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="bd938-194">$destBlobName</span></span>|<span data-ttu-id="bd938-195">Si tratta di nome di blob di output di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-195">This is hello output blob name.</span></span> <span data-ttu-id="bd938-196">valore predefinito di Hello è **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="bd938-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="bd938-197">Se si modifica il valore di predefinito hello, è necessario pertanto gli script di Windows PowerShell hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="bd938-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="bd938-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="bd938-198">$trackString</span></span>|<span data-ttu-id="bd938-199">servizio web Hello restituirà le parole chiave correlate toothese TWEET.</span><span class="sxs-lookup"><span data-stu-id="bd938-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="bd938-200">valore predefinito di Hello è **HDInsight di Azure, Cloud,**.</span><span class="sxs-lookup"><span data-stu-id="bd938-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="bd938-201">Se si modifica il valore di predefinito hello, sarà necessario aggiornare gli script di PowerShell di Windows hello conseguenza.</span><span class="sxs-lookup"><span data-stu-id="bd938-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="bd938-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="bd938-202">$lineMax</span></span>|<span data-ttu-id="bd938-203">il valore di Hello determina quanti TWEET hello script leggerà.</span><span class="sxs-lookup"><span data-stu-id="bd938-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="bd938-204">Sono necessari circa tre minuti tooread 100 TWEET.</span><span class="sxs-lookup"><span data-stu-id="bd938-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="bd938-205">È possibile impostare un numero maggiore, ma richiederà più toodownload ora.</span><span class="sxs-lookup"><span data-stu-id="bd938-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="bd938-206">Premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="bd938-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="bd938-207">Se si verificano problemi, in alternativa, selezionare tutte le righe hello e quindi premere **F8**.</span><span class="sxs-lookup"><span data-stu-id="bd938-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="bd938-208">Alla fine dell'output verrà visualizzato</span><span class="sxs-lookup"><span data-stu-id="bd938-208">You shall see "Complete!"</span></span> <span data-ttu-id="bd938-209">alla fine di hello dell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-209">at hello end of hello output.</span></span> <span data-ttu-id="bd938-210">Eventuali messaggi di errore verranno visualizzati in rosso.</span><span class="sxs-lookup"><span data-stu-id="bd938-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="bd938-211">Come procedura di convalida, è possibile controllare il file di output di hello, **/tutorials/twitter/data/tweets.txt**, alla risorsa di archiviazione Blob di Azure usando un Esplora archivi Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd938-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="bd938-212">Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="bd938-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="bd938-213">Creare uno script HiveQL</span><span class="sxs-lookup"><span data-stu-id="bd938-213">Create HiveQL script</span></span>
<span data-ttu-id="bd938-214">Con Azure PowerShell, è possibile eseguire più istruzioni HiveQL uno alla volta oppure hello pacchetto HiveQL istruzione in un file di script.</span><span class="sxs-lookup"><span data-stu-id="bd938-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="bd938-215">In questa esercitazione verrà creato uno script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="bd938-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="bd938-216">file di script Hello deve essere tooAzure caricato nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="bd938-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="bd938-217">Nella sezione successiva hello, si eseguirà il file di script hello tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd938-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="bd938-218">file di script Hive Hello e un file contenente 10.000 TWEET sono stati caricati in un contenitore di Blob pubblico.</span><span class="sxs-lookup"><span data-stu-id="bd938-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="bd938-219">È possibile ignorare questa sezione se si desidera toouse hello caricamento file.</span><span class="sxs-lookup"><span data-stu-id="bd938-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="bd938-220">Hello script HiveQL eseguirà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="bd938-221">**Elimina tabella tweets_raw hello** nel caso in cui hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="bd938-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="bd938-222">**Creare una tabella Hive di hello tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="bd938-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="bd938-223">Questa tabella strutturata Hive temporanea contiene i dati di hello per ulteriormente estrarre, trasformare e caricare l'elaborazione (ETL).</span><span class="sxs-lookup"><span data-stu-id="bd938-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="bd938-224">Per informazioni sulle partizioni, vedere [Hive tutorial][apache-hive-tutorial] (Esercitazione su Hive).</span><span class="sxs-lookup"><span data-stu-id="bd938-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="bd938-225">**Caricare i dati** dalla cartella di origine hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="bd938-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="bd938-226">Hello TWEET grandi set di dati in formato JSON nidificato a questo punto è stata trasformata in una struttura di tabella temporanea Hive.</span><span class="sxs-lookup"><span data-stu-id="bd938-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="bd938-227">**Eliminazione hello TWEET tabella** nel caso in cui hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="bd938-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="bd938-228">**Creare una tabella TWEET hello**.</span><span class="sxs-lookup"><span data-stu-id="bd938-228">**Create hello tweets table**.</span></span> <span data-ttu-id="bd938-229">È possibile eseguire una query sul set di dati TWEET hello utilizzando Hive, è necessario toorun un altro processo ETL.</span><span class="sxs-lookup"><span data-stu-id="bd938-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="bd938-230">Questo processo ETL definisce uno schema di tabella più dettagliato per i dati archiviati nella tabella "twitter_raw" hello hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="bd938-231">**Inserire la tabella di sovrascrittura**.</span><span class="sxs-lookup"><span data-stu-id="bd938-231">**Insert overwrite table**.</span></span> <span data-ttu-id="bd938-232">Questo script Hive complesso provoca un set di processi MapReduce lungo da un cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="bd938-233">A seconda del set di dati e hello delle dimensioni del cluster, l'operazione potrebbe richiedere circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="bd938-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="bd938-234">**Inserire la directory di sovrascrittura**.</span><span class="sxs-lookup"><span data-stu-id="bd938-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="bd938-235">Eseguire una query e output hello dataset tooa un file.</span><span class="sxs-lookup"><span data-stu-id="bd938-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="bd938-236">Questa query restituirà un elenco di utenti di Twitter che ha inviato la maggior parte dei TWEET contenenti la parola hello "Azure".</span><span class="sxs-lookup"><span data-stu-id="bd938-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="bd938-237">**un Hive toocreate script e caricarlo tooAzure**</span><span class="sxs-lookup"><span data-stu-id="bd938-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="bd938-238">Aprire Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="bd938-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="bd938-239">Copiare lo script seguente nel riquadro di script hello hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-239">Copy hello following script into hello script pane:</span></span>

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="bd938-240">Impostare hello innanzitutto due variabili nello script hello:</span><span class="sxs-lookup"><span data-stu-id="bd938-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="bd938-241">Variabile</span><span class="sxs-lookup"><span data-stu-id="bd938-241">Variable</span></span> | <span data-ttu-id="bd938-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bd938-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="bd938-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="bd938-243">$clusterName</span></span> |<span data-ttu-id="bd938-244">Immettere nome del cluster HDInsight hello in cui si desidera un'applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="bd938-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="bd938-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="bd938-245">$subscriptionID</span></span> |<span data-ttu-id="bd938-246">Inserire L'ID della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd938-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="bd938-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="bd938-247">$sourceDataPath</span></span> |<span data-ttu-id="bd938-248">percorso di archiviazione Blob di Azure in cui le query Hive hello verranno leggere i dati hello Hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="bd938-249">Non è necessario toochange questa variabile.</span><span class="sxs-lookup"><span data-stu-id="bd938-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="bd938-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="bd938-250">$outputPath</span></span> |<span data-ttu-id="bd938-251">percorso di archiviazione Blob di Azure in cui le query Hive hello fornirà risultati hello Hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="bd938-252">Non è necessario toochange questa variabile.</span><span class="sxs-lookup"><span data-stu-id="bd938-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="bd938-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="bd938-253">$hqlScriptFile</span></span> |<span data-ttu-id="bd938-254">percorso di Hello e il nome di file hello hello HiveQL del file di script.</span><span class="sxs-lookup"><span data-stu-id="bd938-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="bd938-255">Non è necessario toochange questa variabile.</span><span class="sxs-lookup"><span data-stu-id="bd938-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="bd938-256">Premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="bd938-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="bd938-257">Se si verificano problemi, in alternativa, selezionare tutte le righe hello e quindi premere **F8**.</span><span class="sxs-lookup"><span data-stu-id="bd938-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="bd938-258">Alla fine dell'output verrà visualizzato</span><span class="sxs-lookup"><span data-stu-id="bd938-258">You shall see "Complete!"</span></span> <span data-ttu-id="bd938-259">alla fine di hello dell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-259">at hello end of hello output.</span></span> <span data-ttu-id="bd938-260">Eventuali messaggi di errore verranno visualizzati in rosso.</span><span class="sxs-lookup"><span data-stu-id="bd938-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="bd938-261">Come procedura di convalida, è possibile controllare il file di output di hello, **/tutorials/twitter/twitter.hql**, alla risorsa di archiviazione Blob di Azure usando un Esplora archivi Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd938-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="bd938-262">Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="bd938-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="bd938-263">Elaborare i dati di Twitter tramite Hive</span><span class="sxs-lookup"><span data-stu-id="bd938-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="bd938-264">Tutte le operazioni di preparazione hello completata.</span><span class="sxs-lookup"><span data-stu-id="bd938-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="bd938-265">A questo punto, è possibile richiamare script Hive hello e controllare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="bd938-266">Inviare un processo Hive</span><span class="sxs-lookup"><span data-stu-id="bd938-266">Submit a Hive job</span></span>
<span data-ttu-id="bd938-267">Utilizzare lo script Hive di Windows PowerShell script toorun hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="bd938-268">È necessario prima variabile di tooset hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="bd938-269">hello toouse TWEET e script HiveQL caricato hello ultime due sezioni, set $hqlScriptFile too"/tutorials/twitter/twitter.hql hello".</span><span class="sxs-lookup"><span data-stu-id="bd938-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="bd938-270">hello toouse quelli che sono stati caricati blob pubblici tooa, impostare $hqlScriptFile troppo"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="bd938-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
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

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="bd938-271">Controllare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="bd938-271">Check hello results</span></span>
<span data-ttu-id="bd938-272">Utilizzare hello seguente hello toocheck di Windows PowerShell script Hive output del processo.</span><span class="sxs-lookup"><span data-stu-id="bd938-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="bd938-273">È necessario innanzitutto due variabili di tooset hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
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
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabella Hive Hello utilizza \001 come hello delimitatore di campo. <span data-ttu-id="bd938-275">delimitatore di Hello non è visibile nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="bd938-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="bd938-276">Dopo che i risultati dell'analisi hello vengono inseriti nell'archiviazione Blob di Azure, è possibile esportare hello dati tooan Azure SQL database di SQL server, esportare hello dati tooExcel tramite Power Query o la connessione dati toohello dell'applicazione utilizzando hello Hive Driver ODBC.</span><span class="sxs-lookup"><span data-stu-id="bd938-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="bd938-277">Per ulteriori informazioni, vedere [utilizzare Sqoop con HDInsight][hdinsight-use-sqoop], [analizza i dati di ritardo di volo con HDInsight][hdinsight-analyze-flight-delay-data], [ Connettere Excel tooHDInsight con Power Query][hdinsight-power-query], e [tooHDInsight connessione Excel con il Driver ODBC di Hive Microsoft hello][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="bd938-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd938-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd938-278">Next steps</span></span>
<span data-ttu-id="bd938-279">In questa esercitazione abbiamo visto come tootransform un set di dati non strutturati JSON in un tooquery di tabella Hive strutturata, esplorare e analizzare i dati da Twitter usando HDInsight in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd938-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="bd938-280">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="bd938-280">toolearn more, see:</span></span>

* <span data-ttu-id="bd938-281">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="bd938-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="bd938-282">[Analizzare i sentimenti Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="bd938-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="bd938-283">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="bd938-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="bd938-284">[Connettere Excel tooHDInsight con Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="bd938-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="bd938-285">[Connettere Excel tooHDInsight con il Driver ODBC di Hive Microsoft hello][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="bd938-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="bd938-286">[Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="bd938-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
