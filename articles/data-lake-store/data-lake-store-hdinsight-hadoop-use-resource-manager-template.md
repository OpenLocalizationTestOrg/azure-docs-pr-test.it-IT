---
title: Usare modelli di Azure per creare istanze di HDInsight e Data Lake Store | Documentazione Microsoft
description: Usare un modello di Azure Resource Manager per creare e usare cluster HDInsight con Azure Data Lake Store
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="35062-103">Creare un cluster HDInsight con Data Lake Store usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35062-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35062-104">Uso del portale</span><span class="sxs-lookup"><span data-stu-id="35062-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="35062-105">Uso di PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="35062-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="35062-106">Uso di PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="35062-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="35062-107">Utilizzo di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35062-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="35062-108">Informazioni su come usare Azure PowerShell per configurare un cluster HDInsight con Azure Data Lake Store **come risorsa di archiviazione aggiuntiva**.</span><span class="sxs-lookup"><span data-stu-id="35062-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="35062-109">Per i tipi di cluster supportati, Data Lake Store deve essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="35062-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="35062-110">Quando Data Lake Store viene usato come risorsa di archiviazione aggiuntiva, l'account di archiviazione predefinito per i cluster saranno i BLOB del servizio di archiviazione di Azure (WASB) e i file correlati ai cluster (ad esempio log e così via) vengono scritti nella risorsa di archiviazione predefinita, mentre i dati da elaborare possono essere archiviati in un account di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35062-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="35062-111">L'uso di Archivio Data Lake come account di archiviazione aggiuntivo non ha impatto sulle prestazioni o sulla possibilità di leggere/scrivere nella risorsa di archiviazione dal cluster.</span><span class="sxs-lookup"><span data-stu-id="35062-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="35062-112">Udo di Data Lake Store per l'archiviazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="35062-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="35062-113">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="35062-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="35062-114">L'opzione per creare cluster HDInsight con accesso a Data Lake Store come risorsa di archiviazione predefinita è disponibile per HDInsight versione 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="35062-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="35062-115">L'opzione per creare cluster HDInsight con accesso a Data Lake Store come risorsa di archiviazione aggiuntiva è disponibile per HDInsight versioni 3.2, 3.4, 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="35062-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="35062-116">In questo articolo si effettuerà il provisioning di un cluster Hadoop con Archivio Data Lake come risorsa di archiviazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="35062-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="35062-117">Per istruzioni su come creare un cluster Hadoop con Data Lake Store come risorsa di archiviazione predefinita, vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35062-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35062-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35062-118">Prerequisites</span></span>
<span data-ttu-id="35062-119">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="35062-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="35062-120">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="35062-120">**An Azure subscription**.</span></span> <span data-ttu-id="35062-121">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35062-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35062-122">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="35062-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="35062-123">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35062-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="35062-124">**Entità servizio di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35062-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="35062-125">Questa esercitazione fornisce tutte le istruzioni utili su come creare un'entità servizio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35062-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="35062-126">Tuttavia, è necessario essere un amministratore di Azure AD per creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="35062-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="35062-127">Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e procedere con l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="35062-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="35062-128">**Se non si è un amministratore di Azure AD**, non sarà possibile eseguire i passaggi necessari per creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="35062-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="35062-129">In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35062-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="35062-130">Inoltre, l'entità servizio deve essere creata usando un certificato, come descritto in [Creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="35062-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="35062-131">Creare un cluster HDInsight con Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="35062-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="35062-132">Il modello di Resource Manager e i prerequisiti per l'uso del modello sono disponibili in GitHub alla sezione [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage) (Distribuzione di un cluster HDInsight Linux con il nuovo Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="35062-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="35062-133">Seguire le istruzioni riportate in questa pagina per creare un cluster HDInsight con Azure Data Lake Store come spazio di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="35062-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="35062-134">Le istruzioni indicate nella suddetta pagina richiedono PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35062-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="35062-135">Prima di mettere in pratica queste istruzioni, assicurarsi di accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="35062-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="35062-136">Sul desktop aprire una nuova finestra di Azure PowerShell e immettere i frammenti di codice seguenti.</span><span class="sxs-lookup"><span data-stu-id="35062-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="35062-137">Quando viene richiesto di effettuare l'accesso, assicurarsi di accedere come amministratore/proprietario della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="35062-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="35062-138">Caricare i dati di esempio in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="35062-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="35062-139">Il modello di Resource Manager crea un nuovo account Data Lake Store e lo associa al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35062-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="35062-140">È ora necessario caricare alcuni dati di esempio in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35062-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="35062-141">Questi dati saranno necessari più avanti nell'esercitazione per eseguire i processi da un cluster HDInsight che accede ai dati nell'Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="35062-142">Per istruzioni su come caricare i dati, vedere [Caricare dati in Archivio Data Lake di Azure](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="35062-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="35062-143">Se si stanno cercando dati di esempio da caricare, è possibile ottenere la cartella **Ambulance Data** dal [Repository GitHub per Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="35062-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="35062-144">Impostare ACL rilevanti per i dati di esempio</span><span class="sxs-lookup"><span data-stu-id="35062-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="35062-145">Per assicurarsi che i dati di esempio caricati siano accessibili dal cluster HDInsight, è necessario assicurarsi che l'applicazione Azure AD usata per stabilire l'identità tra il cluster HDInsight e Data Lake Store disponga dell'accesso al file o alla cartella a cui si sta tentando di accedere.</span><span class="sxs-lookup"><span data-stu-id="35062-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="35062-146">A questo scopo, eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="35062-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="35062-147">Trovare il nome dell'applicazione Azure AD associata al cluster HDInsight e Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35062-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="35062-148">Per ricercare il nome è possibile aprire il pannello del cluster HDInsight creato usando il modello di Resource Manager, fare clic sulla scheda **Identità AAD del cluster** e cercare il valore **Nome visualizzato dell'entità servizio**.</span><span class="sxs-lookup"><span data-stu-id="35062-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="35062-149">A questo punto, consentire all'applicazione di Azure AD di accedere al file o alla cartella a cui si desidera accedere dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35062-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="35062-150">Per impostare gli ACL corretti sul file o sulla cartella in Data Lake Store, vedere [Protezione dei dati presenti in Archivio Data Lake di Azure](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="35062-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="35062-151">Eseguire i processi di test sul cluster HDInsight per usare Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="35062-152">Dopo aver configurato un cluster HDInsight, è possibile eseguire processi di test sul cluster per verificare che il cluster HDInsight possa accedere ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="35062-153">A questo scopo, verrà eseguito un processo Hive di esempio che crea una tabella con i dati di esempio caricati in precedenza in Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="35062-154">In questa sezione si accede tramite SSH a un cluster Linux HDInsight e si esegue una query Hive di esempio.</span><span class="sxs-lookup"><span data-stu-id="35062-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="35062-155">Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="35062-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="35062-156">Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="35062-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="35062-157">Dopo la connessione, avviare l'interfaccia della riga di comando di Hive mediante il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="35062-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="35062-158">Usando l'interfaccia della riga di comando, immettere le istruzioni seguenti per creare una nuova tabella denominata **vehicles** con i dati di esempio in Archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="35062-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="35062-159">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="35062-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="35062-160">Accedere ad Archivio Data Lake tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="35062-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="35062-161">Dopo aver configurato il cluster HDInsight perché funzioni con Archivio Data Lake, è possibile usare i comandi della shell HDFS per accedere all'archivio.</span><span class="sxs-lookup"><span data-stu-id="35062-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="35062-162">In questa sezione si accede tramite SSH a un cluster Linux HDInsight e si eseguono comandi HDFS.</span><span class="sxs-lookup"><span data-stu-id="35062-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="35062-163">Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="35062-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="35062-164">Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="35062-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="35062-165">Dopo avere stabilito la connessione, usare il comando del file system HDFS seguente per elencare i file nell'Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="35062-166">Dovrebbe essere elencato anche il file precedentemente caricato in Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35062-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="35062-167">È inoltre possibile usare il comando `hdfs dfs -put` per caricare dei file in Archivio Data Lake e quindi usare `hdfs dfs -ls` per verificare che i file siano stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="35062-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="35062-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35062-168">Next steps</span></span>
* [<span data-ttu-id="35062-169">Copiare i dati dai BLOB del servizio di archiviazione di Azure in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="35062-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
