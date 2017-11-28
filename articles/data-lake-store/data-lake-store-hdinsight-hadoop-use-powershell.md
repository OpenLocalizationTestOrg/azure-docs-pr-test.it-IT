---
title: 'PowerShell: Cluster HDInsight di Azure con Data Lake Store come risorsa di archiviazione aggiuntiva | Documentazione Microsoft'
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d31c1-102">Usare Azure PowerShell per creare un cluster HDInsight con Data Lake Store (come risorsa di archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="d31c1-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d31c1-103">Uso del portale</span><span class="sxs-lookup"><span data-stu-id="d31c1-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="d31c1-104">Uso di PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="d31c1-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="d31c1-105">Uso di PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="d31c1-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="d31c1-106">Utilizzo di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d31c1-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="d31c1-107">Informazioni su come usare Azure PowerShell per configurare un cluster HDInsight con Azure Data Lake Store **come risorsa di archiviazione aggiuntiva**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="d31c1-108">Per istruzioni su come creare un cluster HDInsight con Azure Data Lake Store come risorsa di archiviazione predefinita, vedere [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md) (Creare un cluster HDInsight con Data Lake Store come risorsa di archiviazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="d31c1-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d31c1-109">Se si prevede di usare Azure Data Lake Store come risorsa di archiviazione aggiuntiva per i cluster HDInsight, è vivamente consigliabile farlo durante la creazione del cluster, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d31c1-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="d31c1-110">L'aggiunta di Azure Data Lake Store come risorsa di archiviazione aggiuntiva a un cluster HDInsight esistente è un processo complesso e soggetto a errori.</span><span class="sxs-lookup"><span data-stu-id="d31c1-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="d31c1-111">Per i tipi di cluster supportati, Data Lake Store può essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="d31c1-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="d31c1-112">Quando Data Lake Store viene usato come risorsa di archiviazione aggiuntiva, l'account di archiviazione predefinito per i cluster saranno i BLOB del servizio di archiviazione di Azure (WASB) e i file correlati ai cluster (ad esempio log e così via) vengono scritti nella risorsa di archiviazione predefinita, mentre i dati da elaborare possono essere archiviati in un account di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d31c1-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="d31c1-113">L'uso di Archivio Data Lake come account di archiviazione aggiuntivo non ha impatto sulle prestazioni o sulla possibilità di leggere/scrivere nella risorsa di archiviazione dal cluster.</span><span class="sxs-lookup"><span data-stu-id="d31c1-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="d31c1-114">Udo di Data Lake Store per l'archiviazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="d31c1-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="d31c1-115">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="d31c1-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="d31c1-116">L'opzione per creare cluster HDInsight con accesso a Data Lake Store come risorsa di archiviazione aggiuntiva è disponibile per le versioni 3.2, 3.4, 3.5 e 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d31c1-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="d31c1-117">La configurazione di HDInsight perché funzioni con Archivio Data Lake tramite PowerShell prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d31c1-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="d31c1-118">Creare un Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="d31c1-119">Configurare l'autenticazione per l'accesso basato sui ruoli all'Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="d31c1-120">Creare un cluster HDInsight con l'autenticazione per Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="d31c1-121">Eseguire un processo di test sul cluster</span><span class="sxs-lookup"><span data-stu-id="d31c1-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d31c1-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d31c1-122">Prerequisites</span></span>
<span data-ttu-id="d31c1-123">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d31c1-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d31c1-124">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-124">**An Azure subscription**.</span></span> <span data-ttu-id="d31c1-125">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d31c1-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d31c1-126">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="d31c1-127">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d31c1-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d31c1-128">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-128">**Windows SDK**.</span></span> <span data-ttu-id="d31c1-129">Per installarlo, fare clic [qui](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="d31c1-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="d31c1-130">Usarlo per creare un certificato di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d31c1-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="d31c1-131">**Entità servizio di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="d31c1-132">Questa esercitazione fornisce tutte le istruzioni utili su come creare un'entità servizio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d31c1-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="d31c1-133">Tuttavia, è necessario essere un amministratore di Azure AD per creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d31c1-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="d31c1-134">Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e procedere con l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d31c1-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="d31c1-135">**Se non si è un amministratore di Azure AD**, non sarà possibile eseguire i passaggi necessari per creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d31c1-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="d31c1-136">In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d31c1-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="d31c1-137">Inoltre, l'entità servizio deve essere creata usando un certificato, come descritto in [Creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="d31c1-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="d31c1-138">Creare un Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="d31c1-139">Per creare un Archivio Data Lake, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="d31c1-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="d31c1-140">Sul desktop aprire una nuova finestra di Azure PowerShell e immettere il frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="d31c1-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="d31c1-141">Quando viene richiesto di effettuare l'accesso, assicurarsi di accedere come amministratore/proprietario della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="d31c1-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="d31c1-142">Se si riceve un errore simile a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` quando si registra il provider di risorse Data Lake Store, è possibile che la sottoscrizione non sia abilitata per Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d31c1-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="d31c1-143">Assicurarsi di abilitare la sottoscrizione di Azure per l'anteprima pubblica di Archivio Data Lake seguendo queste [istruzioni](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d31c1-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="d31c1-144">Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d31c1-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="d31c1-145">Per iniziare, creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d31c1-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="d31c1-146">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d31c1-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="d31c1-147">Creare un account Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="d31c1-148">Il nome dell'account specificato deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="d31c1-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="d31c1-149">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d31c1-149">You should see an output like the following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="d31c1-150">Caricare alcuni dati di esempio in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="d31c1-151">Questi dati saranno usati più avanti in questo articolo per verificare che siano accessibili da un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d31c1-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="d31c1-152">Se si stanno cercando dati di esempio da caricare, è possibile ottenere la cartella **Ambulance Data** dal [Repository GitHub per Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="d31c1-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="d31c1-153">Configurare l'autenticazione per l'accesso basato sui ruoli all'Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="d31c1-154">Ogni sottoscrizione di Azure è associata a una Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d31c1-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="d31c1-155">Gli utenti e i servizi che accedono alle risorse della sottoscrizione tramite il portale di Azure classico o l'API di Azure Resource Manager devono prima autenticarsi con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d31c1-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="d31c1-156">L'accesso viene concesso alle sottoscrizioni e ai servizi di Azure tramite l'assegnazione del ruolo appropriato in una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="d31c1-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="d31c1-157">Per i servizi, un'entità servizio identifica il servizio in Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d31c1-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="d31c1-158">Questa sezione illustra come concedere a un servizio dell'applicazione, ad esempio HDInsight, l'accesso a una risorsa di Azure, ovvero l'account Archivio Azure Data Lake creato in precedenza, mediante la creazione di un'entità servizio per l'applicazione e l'assegnazione di ruoli a tale entità con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d31c1-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="d31c1-159">Per configurare l'autenticazione di Active Directory per Azure Data Lake, è necessario eseguire queste attività.</span><span class="sxs-lookup"><span data-stu-id="d31c1-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="d31c1-160">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d31c1-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="d31c1-161">Creare un'applicazione in Azure Active Directory e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="d31c1-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d31c1-162">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d31c1-162">Create a self-signed certificate</span></span>
<span data-ttu-id="d31c1-163">Assicurarsi di avere installato [Windows SDK](https://dev.windows.com/en-us/downloads) prima di continuare con i passaggi descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d31c1-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="d31c1-164">È necessario aver creato anche una directory, ad esempio **C:\mycertdir**, in cui sarà creato il certificato.</span><span class="sxs-lookup"><span data-stu-id="d31c1-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="d31c1-165">Dalla finestra di PowerShell passare al percorso in cui è installato Windows SDK, in genere `C:\Program Files (x86)\Windows Kits\10\bin\x86`, e usare l'utilità [MakeCert][makecert] per creare un certificato autofirmato e una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d31c1-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="d31c1-166">Usare il comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d31c1-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="d31c1-167">Verrà richiesto di immettere la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d31c1-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="d31c1-168">Una volta completata l'esecuzione del comando, nella directory del certificato specificata verranno visualizzati **CertFile.cer** e **mykey.pvk**.</span><span class="sxs-lookup"><span data-stu-id="d31c1-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="d31c1-169">Usare l'utilità [Pvk2Pfx][pvk2pfx] per convertire i file con estensione PVK e CER creati da MakeCert in un file con estensione PFX.</span><span class="sxs-lookup"><span data-stu-id="d31c1-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="d31c1-170">Eseguire il comando indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d31c1-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="d31c1-171">Quando richiesto immettere la password della chiave privata specificata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d31c1-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="d31c1-172">Il valore specificato per il parametro **-po** è la password associata al file PFX.</span><span class="sxs-lookup"><span data-stu-id="d31c1-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="d31c1-173">Dopo il completamento del comando, nella directory del certificato specificata dovrebbe essere visualizzato un file denominato CertFile.pfx.</span><span class="sxs-lookup"><span data-stu-id="d31c1-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="d31c1-174">Creare un'applicazione Azure Active Directory e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="d31c1-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="d31c1-175">In questa sezione seguire la procedura per creare un'entità servizio per un'applicazione Azure Active Directory, assegnare un ruolo all'entità servizio e autenticarsi come entità servizio fornendo un certificato.</span><span class="sxs-lookup"><span data-stu-id="d31c1-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="d31c1-176">Eseguire i comandi seguenti per creare un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d31c1-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="d31c1-177">Incollare i cmdlet seguenti nella finestra della console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d31c1-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="d31c1-178">Assicurarsi che il valore specificato per la proprietà **-DisplayName** sia univoco.</span><span class="sxs-lookup"><span data-stu-id="d31c1-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="d31c1-179">I valori per **-HomePage** e **-IdentiferUris** sono valori segnaposto e non vengono verificati.</span><span class="sxs-lookup"><span data-stu-id="d31c1-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="d31c1-180">Creare un'entità servizio usando l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="d31c1-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="d31c1-181">Concedere l'accesso dell'entità servizio al file e alla cartella Data Lake Store a cui si vuole accedere dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d31c1-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="d31c1-182">Il frammento seguente consente di accedere alla root dell'account Data Lake Store in cui è stato copiato il file di dati di esempio e al file stesso.</span><span class="sxs-lookup"><span data-stu-id="d31c1-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d31c1-183">Creare un cluster HDInsight Linux con Data Lake Store come risorsa di archiviazione aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="d31c1-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="d31c1-184">In questa sezione viene creato un cluster HDInsight di Handoop Linux con Data Lake Store come risorsa di archiviazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="d31c1-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="d31c1-185">Per questa versione il cluster HDInsight e Data Lake Store devono trovarsi nella stessa località.</span><span class="sxs-lookup"><span data-stu-id="d31c1-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="d31c1-186">Iniziare recuperando l'ID tenant della sottoscrizione,</span><span class="sxs-lookup"><span data-stu-id="d31c1-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="d31c1-187">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="d31c1-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="d31c1-188">In questa versione Archivio Data Lake può essere usato solo come risorsa di archiviazione aggiuntiva per un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d31c1-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="d31c1-189">L'archivio predefinito continuerà a essere BLOB di archiviazione di Azure (WABS).</span><span class="sxs-lookup"><span data-stu-id="d31c1-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="d31c1-190">Si procederà quindi prima di tutto alla creazione dell'account di archiviazione e dei contenitori di archiviazione richiesti per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d31c1-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="d31c1-191">Creare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d31c1-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="d31c1-192">Eseguire i cmdlet seguenti.</span><span class="sxs-lookup"><span data-stu-id="d31c1-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="d31c1-193">Dopo il completamento del cmdlet, viene visualizzato un output simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="d31c1-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="d31c1-194">Eseguire i processi di test sul cluster HDInsight per usare Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="d31c1-195">Dopo aver configurato un cluster HDInsight, è possibile eseguire processi di test sul cluster per verificare che il cluster HDInsight possa accedere ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="d31c1-196">A questo scopo, verrà eseguito un processo Hive di esempio che crea una tabella con i dati di esempio caricati in precedenza in Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="d31c1-197">In questa sezione si accede tramite SSH al cluster Linux HDInsight e viene eseguita una query Hive di esempio.</span><span class="sxs-lookup"><span data-stu-id="d31c1-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="d31c1-198">Se si usa un client Windows per accedere tramite SSH al cluster, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d31c1-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d31c1-199">Se si usa un client Linux per accedere tramite SSH al cluster, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d31c1-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="d31c1-200">Dopo la connessione, avviare l'interfaccia della riga di comando di Hive mediante il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d31c1-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="d31c1-201">Usando l'interfaccia della riga di comando, immettere le istruzioni seguenti per creare una nuova tabella denominata **vehicles** con i dati di esempio in Archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="d31c1-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="d31c1-202">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d31c1-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="d31c1-203">Accedere ad Archivio Data Lake tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="d31c1-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="d31c1-204">Dopo aver configurato il cluster HDInsight perché funzioni con Archivio Data Lake, è possibile usare i comandi della shell HDFS per accedere all'archivio.</span><span class="sxs-lookup"><span data-stu-id="d31c1-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="d31c1-205">In questa sezione si accede tramite SSH al cluster Linux HDInsight creato e viene eseguito il comando HDFS.</span><span class="sxs-lookup"><span data-stu-id="d31c1-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="d31c1-206">Se si usa un client Windows per accedere tramite SSH al cluster, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d31c1-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d31c1-207">Se si usa un client Linux per accedere tramite SSH al cluster, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d31c1-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="d31c1-208">Dopo avere stabilito la connessione, usare il comando del file system HDFS seguente per elencare i file nell'Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="d31c1-209">Dovrebbe essere elencato anche il file precedentemente caricato in Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d31c1-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="d31c1-210">È inoltre possibile usare il comando `hdfs dfs -put` per caricare dei file in Archivio Data Lake e quindi usare `hdfs dfs -ls` per verificare che i file siano stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="d31c1-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="d31c1-211">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d31c1-211">See Also</span></span>
* [<span data-ttu-id="d31c1-212">Portale: Creare un cluster HDInsight per usare Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d31c1-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
