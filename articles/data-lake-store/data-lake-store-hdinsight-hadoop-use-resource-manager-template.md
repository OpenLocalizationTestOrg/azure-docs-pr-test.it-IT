---
title: aaaUse toocreate di modelli di Azure HDInsight e archivio Data Lake | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure modelli toocreate e cluster HDInsight con archivio Azure Data Lake
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="76acf-103">Creare un cluster HDInsight con Data Lake Store usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76acf-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76acf-104">Uso del portale</span><span class="sxs-lookup"><span data-stu-id="76acf-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="76acf-105">Uso di PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="76acf-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="76acf-106">Uso di PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="76acf-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="76acf-107">Utilizzo di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76acf-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="76acf-108">Informazioni su come toouse Azure PowerShell tooconfigure un HDInsight cluster con archivio Azure Data Lake **come spazio di archiviazione aggiuntivo**.</span><span class="sxs-lookup"><span data-stu-id="76acf-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="76acf-109">Per i tipi di cluster supportati, Data Lake Store deve essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="76acf-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="76acf-110">Quando archivio Data Lake viene utilizzato come spazio di archiviazione aggiuntivo, account di archiviazione hello predefinito per i cluster hello saranno ancora BLOB di archiviazione di Azure (WASB) e i file correlati al cluster hello (ad esempio, i log e così via) vengono scritti ancora spazio di archiviazione predefinito di toohello, mentre quelli di hello che si desidera tooprocess possono essere archiviati in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="76acf-111">Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influisce sulle prestazioni o hello possibilità tooread/scrittura toohello archiviazione dal hello cluster.</span><span class="sxs-lookup"><span data-stu-id="76acf-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="76acf-112">Udo di Data Lake Store per l'archiviazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="76acf-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="76acf-113">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="76acf-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="76acf-114">Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione predefinito è disponibile per HDInsight versione 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="76acf-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="76acf-115">Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione aggiuntivo è disponibile per le versioni 3.2, 3.4, 3.5 e 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76acf-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="76acf-116">In questo articolo si effettuerà il provisioning di un cluster Hadoop con Archivio Data Lake come risorsa di archiviazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="76acf-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="76acf-117">Per istruzioni su come toocreate un Hadoop cluster con archivio Data Lake come spazio di archiviazione predefinito, vedere [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="76acf-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76acf-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76acf-118">Prerequisites</span></span>
<span data-ttu-id="76acf-119">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="76acf-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="76acf-120">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="76acf-120">**An Azure subscription**.</span></span> <span data-ttu-id="76acf-121">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76acf-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="76acf-122">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="76acf-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="76acf-123">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76acf-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="76acf-124">**Entità servizio di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76acf-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="76acf-125">Passaggi di questa esercitazione vengono fornite istruzioni su come toocreate un'entità servizio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76acf-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="76acf-126">Tuttavia, è necessario essere un toocreate di in grado di Azure AD amministratore toobe un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="76acf-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="76acf-127">Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="76acf-128">**Se non si è un amministratore di Azure AD**, non sarà in grado di tooperform hello passaggi necessari toocreate un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="76acf-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="76acf-129">In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="76acf-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="76acf-130">Inoltre, dell'entità servizio hello devono essere creati utilizzando un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="76acf-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="76acf-131">Creare un cluster HDInsight con Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="76acf-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="76acf-132">il modello di gestione risorse di Hello e hello prerequisiti per l'utilizzo di modello hello, sono disponibili in GitHub all'indirizzo [distribuire un cluster HDInsight Linux con nuovo archivio Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="76acf-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="76acf-133">Istruzioni di hello fornito in questo collegamento di toocreate un cluster HDInsight con archivio Azure Data Lake come spazio di archiviazione aggiuntivo hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="76acf-134">istruzioni di Hello hello collegamento indicato in precedenza richiedono PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76acf-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="76acf-135">Prima di iniziare a tali istruzioni, assicurarsi che si accede tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="76acf-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="76acf-136">Dal desktop, aprire una nuova finestra di PowerShell di Azure e immettere i seguenti frammenti di codice hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="76acf-137">Quando richiesto toolog, assicurarsi che si accede con uno dei hello admininistrators/proprietario della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="76acf-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="76acf-138">Caricare l'archivio di esempio dati toohello Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="76acf-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="76acf-139">il modello di gestione risorse di Hello crea un nuovo account archivio Data Lake e lo associa al cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="76acf-140">È ora necessario caricare alcuni toohello di dati di esempio archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="76acf-141">È necessario che questi dati in un secondo momento nei processi di esercitazione toorun di hello da un cluster HDInsight che accedono ai dati in archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="76acf-142">Per istruzioni su come tooupload dati, vedere [caricare tooyour un file archivio Data Lake](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="76acf-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="76acf-143">Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="76acf-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="76acf-144">Impostare gli ACL rilevanti nei dati di esempio hello</span><span class="sxs-lookup"><span data-stu-id="76acf-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="76acf-145">toomake che i dati di esempio hello caricati siano accessibili dal cluster HDInsight hello, è necessario assicurarsi che l'applicazione hello Azure AD identity tooestablish utilizzato tra cluster di HDInsight hello e archivio Data Lake ha accesso toohello file/cartella che si sta durante il tentativo tooaccess.</span><span class="sxs-lookup"><span data-stu-id="76acf-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="76acf-146">toodo, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="76acf-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="76acf-147">Trovare il nome di hello dell'applicazione Azure AD associata al cluster HDInsight hello e hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="76acf-148">Un modo toolook per nome hello pannello cluster HDInsight hello di tooopen creata tramite il modello di gestione risorse di hello, fare clic su hello **identità AAD Cluster** scheda e cercare il valore di hello di **dell'entità servizio Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="76acf-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="76acf-149">A questo punto, fornire accesso toothis applicazione Azure AD sul hello file o sulla cartella che si desidera tooaccess dal cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="76acf-150">il diritto di hello tooset gli ACL sul hello file o sulla cartella in archivio Data Lake, vedere [la protezione dei dati in archivio Data Lake](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="76acf-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="76acf-151">Eseguire i processi di prova in hello toouse di cluster HDInsight hello archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="76acf-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="76acf-152">Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova in hello cluster tootest tale hello HDInsight cluster può accedere l'archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="76acf-153">toodo in tal caso, si verrà eseguito un processo Hive di esempio che crea una tabella utilizzando i dati di esempio hello caricato archivio precedente tooyour Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="76acf-154">In questa sezione sarà possibile SSH in un cluster HDInsight Linux e in esecuzione hello un esempio di query Hive.</span><span class="sxs-lookup"><span data-stu-id="76acf-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="76acf-155">Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="76acf-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="76acf-156">Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="76acf-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="76acf-157">Una volta connessi, è possibile avviare hello Hive CLI utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76acf-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="76acf-158">Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in hello archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="76acf-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="76acf-159">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="76acf-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="76acf-160">Accedere ad Archivio Data Lake tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="76acf-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="76acf-161">Dopo aver configurato archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare hello HDFS shell comandi tooaccess hello archivio.</span><span class="sxs-lookup"><span data-stu-id="76acf-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="76acf-162">In questa sezione sarà possibile SSH in un cluster HDInsight Linux e in esecuzione hello comandi HDFS.</span><span class="sxs-lookup"><span data-stu-id="76acf-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="76acf-163">Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="76acf-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="76acf-164">Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="76acf-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="76acf-165">Una volta connessi, utilizzare i seguenti file HDFS filesystem comando toolist hello in archivio Data Lake hello hello.</span><span class="sxs-lookup"><span data-stu-id="76acf-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="76acf-166">Vengono elencati i file hello caricato archivio precedente toohello Data Lake.</span><span class="sxs-lookup"><span data-stu-id="76acf-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="76acf-167">È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni toohello file archivio Data Lake e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="76acf-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="76acf-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76acf-168">Next steps</span></span>
* [<span data-ttu-id="76acf-169">Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake</span><span class="sxs-lookup"><span data-stu-id="76acf-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
