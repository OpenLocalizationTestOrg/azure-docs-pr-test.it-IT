---
<span data-ttu-id="d78a0-101">titolo: aaa "PowerShell: cluster HDInsight di Azure con archivio Data Lake come spazio di archiviazione aggiuntivo | Servizi Microsoft Docs": lake-dell'archivio dati, hdinsight documentationcenter: ' autore: manager nitinme: jhubbard editor: cgronlun</span><span class="sxs-lookup"><span data-stu-id="d78a0-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="d78a0-102">ms. AssetID: ms. Service 164ada5a-222e-4be2-bd32-e51dbe993bc0: ms. DevLang archivio data lake: ms. topic na: articolo ms. tgt_pltfrm: Workload na: ms. date big data: author 08/06/2017: nitinme</span><span class="sxs-lookup"><span data-stu-id="d78a0-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d78a0-103">Utilizzo di Azure PowerShell toocreate un cluster HDInsight con archivio Data Lake (come ulteriore spazio di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="d78a0-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d78a0-104">Uso del portale</span><span class="sxs-lookup"><span data-stu-id="d78a0-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="d78a0-105">Uso di PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="d78a0-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="d78a0-106">Uso di PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="d78a0-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="d78a0-107">Utilizzo di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d78a0-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="d78a0-108">Informazioni su come toouse Azure PowerShell tooconfigure un HDInsight cluster con archivio Azure Data Lake **come spazio di archiviazione aggiuntivo**.</span><span class="sxs-lookup"><span data-stu-id="d78a0-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="d78a0-109">Per istruzioni su come toocreate un HDInsight cluster con archivio Azure Data Lake come spazio di archiviazione predefinito, vedere [creare un cluster HDInsight con archivio Data Lake come spazio di archiviazione predefinito](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d78a0-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d78a0-110">Se si intende archivio Azure Data Lake di toouse come spazio di archiviazione aggiuntivo per il cluster HDInsight, è consigliabile farlo durante la creazione di cluster hello come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d78a0-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="d78a0-111">Aggiunta archivio Azure Data Lake come tooan ulteriore spazio di archiviazione cluster HDInsight esistente è una complessità del processo e soggetta a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="d78a0-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="d78a0-112">Per i tipi di cluster supportati, Data Lake Store può essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="d78a0-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="d78a0-113">Quando archivio Data Lake viene utilizzato come spazio di archiviazione aggiuntivo, account di archiviazione hello predefinito per i cluster hello saranno ancora BLOB di archiviazione di Azure (WASB) e i file correlati al cluster hello (ad esempio, i log e così via) vengono scritti ancora spazio di archiviazione predefinito di toohello, mentre quelli di hello che si desidera tooprocess possono essere archiviati in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="d78a0-114">Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influisce sulle prestazioni o hello possibilità tooread/scrittura toohello archiviazione dal hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d78a0-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="d78a0-115">Udo di Data Lake Store per l'archiviazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="d78a0-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="d78a0-116">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="d78a0-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="d78a0-117">Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione aggiuntivo è disponibile per le versioni 3.2, 3.4, 3.5 e 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d78a0-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="d78a0-118">La configurazione di HDInsight toowork con archivio Data Lake tramite PowerShell include hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d78a0-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="d78a0-119">Creare un Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d78a0-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="d78a0-120">Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="d78a0-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="d78a0-121">Creare cluster HDInsight con autenticazione tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="d78a0-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="d78a0-122">Eseguire un processo di test in cluster hello</span><span class="sxs-lookup"><span data-stu-id="d78a0-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d78a0-123">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d78a0-123">Prerequisites</span></span>
<span data-ttu-id="d78a0-124">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d78a0-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d78a0-125">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d78a0-125">**An Azure subscription**.</span></span> <span data-ttu-id="d78a0-126">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d78a0-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d78a0-127">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="d78a0-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="d78a0-128">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d78a0-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d78a0-129">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="d78a0-129">**Windows SDK**.</span></span> <span data-ttu-id="d78a0-130">Per installarlo, fare clic [qui](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="d78a0-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="d78a0-131">Utilizzare questo toocreate un certificato di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d78a0-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="d78a0-132">**Entità servizio di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d78a0-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="d78a0-133">Passaggi di questa esercitazione vengono fornite istruzioni su come toocreate un'entità servizio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d78a0-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="d78a0-134">Tuttavia, è necessario essere un toocreate di in grado di Azure AD amministratore toobe un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d78a0-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="d78a0-135">Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="d78a0-136">**Se non si è un amministratore di Azure AD**, non sarà in grado di tooperform hello passaggi necessari toocreate un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d78a0-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="d78a0-137">In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d78a0-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="d78a0-138">Inoltre, dell'entità servizio hello devono essere creati utilizzando un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="d78a0-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="d78a0-139">Creare un Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d78a0-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="d78a0-140">Seguire questi toocreate passaggi un archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="d78a0-141">Dal desktop, aprire una nuova finestra di Azure PowerShell e immettere hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="d78a0-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="d78a0-142">Quando richiesto toolog, assicurarsi che si accede con un proprietario o amministratore della sottoscrizione hello:</span><span class="sxs-lookup"><span data-stu-id="d78a0-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="d78a0-143">Se si riceve un messaggio di errore simile troppo`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` quando si registra provider di risorse di archivio Data Lake hello, è possibile che la sottoscrizione non è abilitata per l'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="d78a0-144">Assicurarsi di abilitare la sottoscrizione di Azure per l'anteprima pubblica di Archivio Data Lake seguendo queste [istruzioni](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d78a0-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="d78a0-145">Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d78a0-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="d78a0-146">Per iniziare, creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d78a0-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="d78a0-147">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d78a0-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="d78a0-148">Creare un account Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="d78a0-149">account Hello nome specificato deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="d78a0-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="d78a0-150">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="d78a0-150">You should see an output like hello following:</span></span>

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

5. <span data-ttu-id="d78a0-151">Caricare alcuni tooAzure di dati di esempio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="d78a0-152">Si userà più avanti in questo articolo di tooverify che dati hello siano accessibili da un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d78a0-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="d78a0-153">Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="d78a0-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="d78a0-154">Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="d78a0-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="d78a0-155">Ogni sottoscrizione di Azure è associata a una Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d78a0-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="d78a0-156">Gli utenti e servizi che accedono a risorse di sottoscrizione hello utilizzando hello portale classico di Azure o API di gestione risorse di Azure devono prima autenticarsi con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d78a0-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="d78a0-157">Accesso tooAzure sottoscrizioni e dei servizi tramite l'assegnazione di ruolo appropriato di hello in una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="d78a0-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="d78a0-158">Per i servizi, un'entità servizio identifica il servizio di hello in hello Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d78a0-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="d78a0-159">In questa sezione viene illustrato come servizio toogrant un'applicazione, ad esempio HDInsight, accesso tooan risorse di Azure (Buongiorno account archivio Azure Data Lake creato in precedenza), creare un'entità servizio per un'applicazione hello e assegnare ruoli toothat tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d78a0-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="d78a0-160">tooset autenticazione di Active Directory per Azure Data Lake, è necessario eseguire hello seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="d78a0-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="d78a0-161">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d78a0-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="d78a0-162">Creare un'applicazione in Azure Active Directory e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="d78a0-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d78a0-163">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d78a0-163">Create a self-signed certificate</span></span>
<span data-ttu-id="d78a0-164">Assicurarsi di avere [Windows SDK](https://dev.windows.com/en-us/downloads) installato prima di procedere con hello i passaggi in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d78a0-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="d78a0-165">È necessario avere anche creato una directory, ad esempio **C:\mycertdir**, in cui verrà creato il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="d78a0-166">Dalla finestra di PowerShell hello passare toohello percorso in cui è installato Windows SDK (in genere, `C:\Program Files (x86)\Windows Kits\10\bin\x86` e utilizzare hello [MakeCert] [ makecert] toocreate utilità un certificato autofirmato e un chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d78a0-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="d78a0-167">Utilizzare hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d78a0-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="d78a0-168">Password della chiave privata hello tooenter richiesta sarà.</span><span class="sxs-lookup"><span data-stu-id="d78a0-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="d78a0-169">Dopo il comando hello viene eseguito correttamente, verrà visualizzato un **CertFile.cer** e **myKey** nella directory di hello certificato specificato.</span><span class="sxs-lookup"><span data-stu-id="d78a0-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="d78a0-170">Hello utilizzare [Pvk2Pfx] [ pvk2pfx] utilità tooconvert hello PVK e con estensione cer file file con estensione pfx creato tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="d78a0-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="d78a0-171">Eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="d78a0-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="d78a0-172">Quando richiesto immettere hello password della chiave privata specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d78a0-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="d78a0-173">valore specificato per hello Hello **- ordine di acquisto** parametro sia hello password associata al file con estensione pfx hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="d78a0-174">Dopo che il comando hello completata correttamente, verrà inoltre visualizzato un CertFile.pfx nella directory di hello certificato specificato.</span><span class="sxs-lookup"><span data-stu-id="d78a0-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="d78a0-175">Creare un'applicazione Azure Active Directory e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="d78a0-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="d78a0-176">In questa sezione, eseguire i passaggi di hello toocreate un'entità servizio per un'applicazione Azure Active Directory, assegnare un'entità servizio di ruolo toohello e l'autenticazione come entità servizio hello fornendo un certificato.</span><span class="sxs-lookup"><span data-stu-id="d78a0-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="d78a0-177">Eseguire hello toocreate i comandi seguenti di un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d78a0-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="d78a0-178">Incollare i seguenti cmdlet nella finestra della console PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="d78a0-179">Verificare che un valore specificato per hello hello **- DisplayName** la proprietà è univoca.</span><span class="sxs-lookup"><span data-stu-id="d78a0-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="d78a0-180">Hello, inoltre, i valori per **home page -** e **- IdentiferUris** sono i valori segnaposto e non vengono verificati.</span><span class="sxs-lookup"><span data-stu-id="d78a0-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

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
2. <span data-ttu-id="d78a0-181">Creare un'entità servizio utilizzando l'ID applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="d78a0-182">Concedere al file hello che saranno accessibili dal cluster HDInsight hello e cartella di archivio Data Lake toohello accesso dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="d78a0-183">frammento di Hello seguente fornisce radice toohello accesso hello (in cui è stata copiata file di dati di esempio hello) dell'account archivio Data Lake e hello file stesso.</span><span class="sxs-lookup"><span data-stu-id="d78a0-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d78a0-184">Creare un cluster HDInsight Linux con Data Lake Store come risorsa di archiviazione aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="d78a0-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="d78a0-185">In questa sezione viene creato un cluster HDInsight di Handoop Linux con Data Lake Store come risorsa di archiviazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="d78a0-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="d78a0-186">Per questa versione, i cluster HDInsight hello e archivio Data Lake di hello devono trovarsi in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="d78a0-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="d78a0-187">Avviare durante il recupero degli ID di hello sottoscrizione tenant.</span><span class="sxs-lookup"><span data-stu-id="d78a0-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="d78a0-188">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="d78a0-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="d78a0-189">Per questa versione, per un cluster Hadoop, archivio Data Lake sono utilizzabili solo come un'ulteriore spazio di archiviazione per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="d78a0-190">spazio di archiviazione predefinito Hello saranno ancora BLOB hello in archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="d78a0-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="d78a0-191">In tal caso, verrà innanzitutto creata hello contenitori di archiviazione e l'account di archiviazione necessari per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="d78a0-192">Creare cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="d78a0-193">Utilizzare hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="d78a0-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="d78a0-194">Al termine cmdlet hello è stata completata correttamente, verrà visualizzato un output elenca i dettagli del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="d78a0-195">Eseguire i processi di prova in hello toouse di cluster HDInsight hello archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d78a0-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="d78a0-196">Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova in hello cluster tootest tale hello HDInsight cluster può accedere l'archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="d78a0-197">toodo in tal caso, si verrà eseguito un processo Hive di esempio che crea una tabella utilizzando i dati di esempio hello caricato archivio precedente tooyour Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="d78a0-198">In questa sezione sarà possibile SSH in HDInsight Linux cluster creato e l'esecuzione di una query Hive esempio hello hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="d78a0-199">Se si utilizza un tooSSH di client Windows in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d78a0-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d78a0-200">Se si utilizza un tooSSH client Linux in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d78a0-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="d78a0-201">Una volta connessi, è possibile avviare hello Hive CLI utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d78a0-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="d78a0-202">Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in hello archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="d78a0-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="d78a0-203">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="d78a0-203">You should see an output similar toohello following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="d78a0-204">Accedere ad Archivio Data Lake tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="d78a0-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="d78a0-205">Dopo aver configurato archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare hello HDFS shell comandi tooaccess hello archivio.</span><span class="sxs-lookup"><span data-stu-id="d78a0-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="d78a0-206">In questa sezione sarà possibile SSH in HDInsight Linux cluster creato e di eseguire comandi HDFS hello hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="d78a0-207">Se si utilizza un tooSSH di client Windows in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d78a0-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d78a0-208">Se si utilizza un tooSSH client Linux in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d78a0-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="d78a0-209">Una volta connessi, utilizzare i seguenti file HDFS filesystem comando toolist hello in archivio Data Lake hello hello.</span><span class="sxs-lookup"><span data-stu-id="d78a0-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="d78a0-210">Vengono elencati i file hello caricato archivio precedente toohello Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d78a0-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="d78a0-211">È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni toohello file archivio Data Lake e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="d78a0-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="d78a0-212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d78a0-212">See Also</span></span>
* [<span data-ttu-id="d78a0-213">Portale: Creare un toouse cluster HDInsight archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="d78a0-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
