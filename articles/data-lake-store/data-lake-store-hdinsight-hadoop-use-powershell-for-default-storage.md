---
title: HDInsight aaaCreate cluster con archivio Data Lake come spazio di archiviazione predefinito tramite PowerShell | Microsoft documenti
description: Utilizzare toocreate Azure PowerShell e usare il cluster HDInsight con archivio Azure Data Lake
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="b88ae-103">Creare cluster HDInsight con Data Lake Store come risorsa di archiviazione predefinita usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="b88ae-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b88ae-104">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b88ae-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="b88ae-105">Usare PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="b88ae-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="b88ae-106">Usare PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="b88ae-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="b88ae-107">Usare Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b88ae-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="b88ae-108">Informazioni su come cluster di toouse tooconfigure di Azure PowerShell HDInsight di Azure con l'archivio Azure Data Lake, come spazio di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="b88ae-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="b88ae-109">Per istruzioni su come creare un cluster HDInsight con Data Lake Store come risorsa di archiviazione aggiuntiva, vedere [Usare Azure PowerShell per creare un cluster HDInsight con Data Lake Store (come risorsa di archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="b88ae-110">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="b88ae-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="b88ae-111">cluster di HDInsight toocreate opzione Hello con accesso tooData Lake archivio come spazio di archiviazione predefinito è disponibile per HDInsight versione 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="b88ae-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="b88ae-112">toocreate opzione Hello cluster di HDInsight con accesso tooData Lake archivio come spazio di archiviazione predefinito *non disponibile* per il cluster HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="b88ae-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="b88ae-113">tooconfigure toowork di HDInsight con archivio Data Lake tramite PowerShell, seguire le istruzioni hello hello accanto cinque sezioni.</span><span class="sxs-lookup"><span data-stu-id="b88ae-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b88ae-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b88ae-114">Prerequisites</span></span>
<span data-ttu-id="b88ae-115">Prima di iniziare questa esercitazione, assicurarsi che siano soddisfatti i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="b88ae-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="b88ae-116">**Una sottoscrizione di Azure**: andare troppo[versione di valutazione gratuita di Azure ottenere](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b88ae-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b88ae-117">**Azure PowerShell 1.0 o versione successiva**: vedere [come tooinstall e configurare PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b88ae-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b88ae-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, andare troppo[download e strumenti per Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="b88ae-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="b88ae-119">Hello SDK è toocreate utilizzato un certificato di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b88ae-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="b88ae-120">**Entità servizio di Azure Active Directory**: questa esercitazione viene descritto come toocreate un'entità servizio in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b88ae-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b88ae-121">Tuttavia, toocreate un'entità servizio, è necessario essere un amministratore di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b88ae-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="b88ae-122">Se si è un amministratore, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b88ae-123">È possibile creare un'entità servizio solo se si è un amministratore di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b88ae-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="b88ae-124">Prima di poter creare un cluster HDInsight con Data Lake Store, un amministratore di Azure AD deve creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b88ae-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="b88ae-125">Hello dell'entità servizio deve essere creato con un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="b88ae-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="b88ae-126">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="b88ae-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="b88ae-127">un account archivio Data Lake, toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b88ae-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="b88ae-128">Dal desktop, aprire una finestra di PowerShell e quindi immettere hello i frammenti di codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b88ae-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="b88ae-129">Quando si è richiesta toosign in, Accedi come uno degli amministratori di sottoscrizioni hello o proprietari.</span><span class="sxs-lookup"><span data-stu-id="b88ae-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="b88ae-130">Se si registra provider di risorse di archivio Data Lake hello e ricevere un messaggio di errore simile troppo`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, la sottoscrizione potrebbe non essere abilitata per l'archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b88ae-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="b88ae-131">tooenable la sottoscrizione di Azure per l'anteprima pubblica di archivio Data Lake hello, seguire le istruzioni hello [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="b88ae-132">Un account Data Lake Store è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b88ae-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="b88ae-133">Iniziare creando un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b88ae-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="b88ae-134">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b88ae-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="b88ae-135">Creare un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b88ae-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="b88ae-136">account Hello nome specificato deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="b88ae-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="b88ae-137">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b88ae-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="b88ae-138">L'uso di archivio Data Lake come spazio di archiviazione predefinito richiede toospecify che una radice percorso toowhich hello specifici per i cluster vengono copiati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="b88ae-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="b88ae-139">toocreate un percorso, ovvero **/cluster/hdiadlcluster** nel frammento di codice hello, utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b88ae-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="b88ae-140">Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="b88ae-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="b88ae-141">Ogni sottoscrizione di Azure è associata a un'entità di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b88ae-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="b88ae-142">Utenti e servizi di accedere alle risorse di sottoscrizione utilizzando hello portale Azure oppure hello API di gestione risorse di Azure devono prima autenticarsi con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b88ae-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="b88ae-143">Accesso tooAzure sottoscrizioni e dei servizi tramite l'assegnazione di ruolo appropriato di hello in una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="b88ae-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="b88ae-144">Per i servizi, un'entità servizio identifica il servizio di hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b88ae-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="b88ae-145">In questa sezione viene illustrato come servizio toogrant un'applicazione, ad esempio HDInsight, accesso tooan risorse di Azure (Buongiorno account archivio Data Lake creato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="b88ae-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="b88ae-146">Farlo, creare un servizio principale per un'applicazione hello e assegnare ruoli tooit tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b88ae-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="b88ae-147">tooset autenticazione di Active Directory per Azure Data Lake, eseguire attività di hello in hello nelle due sezioni che seguono.</span><span class="sxs-lookup"><span data-stu-id="b88ae-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b88ae-148">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="b88ae-148">Create a self-signed certificate</span></span>
<span data-ttu-id="b88ae-149">Assicurarsi di avere [Windows SDK](https://dev.windows.com/en-us/downloads) installato prima di procedere con hello i passaggi in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b88ae-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="b88ae-150">È necessario avere anche creato una directory, ad esempio *C:\mycertdir*, in cui creare il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="b88ae-151">Finestra di PowerShell hello, passare toohello percorso in cui è installato Windows SDK (in genere, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e utilizzare hello [MakeCert] [ makecert] toocreate utilità un certificato autofirmato e una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b88ae-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="b88ae-152">Utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b88ae-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="b88ae-153">Password della chiave privata hello tooenter richiesta sarà.</span><span class="sxs-lookup"><span data-stu-id="b88ae-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="b88ae-154">Dopo che il comando hello viene eseguito correttamente, si otterranno **CertFile.cer** e **myKey** nella directory di hello certificato specificato.</span><span class="sxs-lookup"><span data-stu-id="b88ae-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="b88ae-155">Hello utilizzare [Pvk2Pfx] [ pvk2pfx] utilità tooconvert hello PVK e con estensione cer file file con estensione pfx creato tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="b88ae-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="b88ae-156">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b88ae-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="b88ae-157">Quando richiesto, immettere hello password della chiave privata specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b88ae-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="b88ae-158">valore specificato per hello Hello **- ordine di acquisto** parametro sia hello password associata a file con estensione pfx hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="b88ae-159">Dopo il comando hello è stato completato, verrà visualizzato anche un **CertFile.pfx** nella directory di hello certificato specificato.</span><span class="sxs-lookup"><span data-stu-id="b88ae-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="b88ae-160">Creare un'applicazione Azure AD e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b88ae-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="b88ae-161">In questa sezione, creare un'entità servizio per un'applicazione Azure AD, assegnare un'entità servizio di ruolo toohello e l'autenticazione come entità servizio hello fornendo un certificato.</span><span class="sxs-lookup"><span data-stu-id="b88ae-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="b88ae-162">toocreate un'applicazione in Azure AD, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b88ae-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="b88ae-163">Incollare i seguenti cmdlet nella finestra della console PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="b88ae-164">Verificare che tale valore hello specificato per hello **- DisplayName** la proprietà è univoca.</span><span class="sxs-lookup"><span data-stu-id="b88ae-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="b88ae-165">i valori per Hello **- home page** e **- IdentiferUris** sono i valori segnaposto e non vengono verificati.</span><span class="sxs-lookup"><span data-stu-id="b88ae-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="b88ae-166">Creare un'entità servizio utilizzando l'ID applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="b88ae-167">Concedere radice dell'archivio Data Lake toohello accesso dell'entità servizio hello e tutte le cartelle di hello nel percorso radice hello specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b88ae-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="b88ae-168">Utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b88ae-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="b88ae-169">Creare un cluster di HDInsight Linux con archivio Data Lake come spazio di archiviazione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="b88ae-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="b88ae-170">In questa sezione, creare un cluster HDInsight Hadoop Linux con archivio Data Lake come spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="b88ae-171">Per questa versione, hello cluster HDInsight e archivio Data Lake deve trovarsi nella hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="b88ae-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="b88ae-172">Recuperare l'ID tenant di sottoscrizione hello e archiviarlo toouse in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b88ae-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="b88ae-173">Creare cluster HDInsight hello utilizzando hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b88ae-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="b88ae-174">Al termine hello cmdlet è stato completato correttamente, verrà visualizzato un output che elenca i dettagli del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="b88ae-175">Eseguire i processi di prova in hello HDInsight cluster toouse archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="b88ae-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="b88ae-176">Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova su di esso tooensure che possa accedere a archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b88ae-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="b88ae-177">toodo in tal caso, eseguire una toocreate processo Hive di esempio una tabella che utilizza dati di esempio hello sono già disponibili in archivio Data Lake in  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="b88ae-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="b88ae-178">In questa sezione, si stabilisce una connessione Secure Shell (SSH) in hello cluster HDInsight Linux creato e quindi si esegue una query Hive di esempio.</span><span class="sxs-lookup"><span data-stu-id="b88ae-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="b88ae-179">Se si utilizza un toomake di client Windows una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b88ae-180">Se si utilizza un toomake client Linux una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="b88ae-181">Dopo aver effettuato la connessione hello, avviare l'interfaccia della riga di comando di hello Hive (CLI) utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b88ae-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="b88ae-182">Utilizzare prova CLI tooenter prova seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="b88ae-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="b88ae-183">Output della query hello dovrebbe nella console di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="b88ae-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b88ae-184">Hello percorso toohello dati di esempio in hello precedente comando CREATE TABLE sono `adl:///example/data/`, dove `adl:///` è hello cluster radice.</span><span class="sxs-lookup"><span data-stu-id="b88ae-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="b88ae-185">Dopo l'esempio hello di directory principale del cluster hello specificato in questa esercitazione, il comando di hello è `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="b88ae-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="b88ae-186">È possibile utilizzare l'alternativa più breve hello o fornire principale del cluster toohello percorso completo di hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="b88ae-187">Accedere a Data Lake Store tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="b88ae-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="b88ae-188">Dopo aver configurato l'archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare l'archivio di hello tooaccess di Hadoop Distributed File System (HDFS) shell dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b88ae-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="b88ae-189">In questa sezione, si effettua una connessione SSH in hello cluster HDInsight Linux creato e quindi eseguire i comandi HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="b88ae-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="b88ae-190">Se si utilizza un toomake di client Windows una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b88ae-191">Se si utilizza un toomake client Linux una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b88ae-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="b88ae-192">Dopo aver effettuato la connessione hello, elenco file hello in archivio Data Lake tramite hello HDFS file system comando seguente.</span><span class="sxs-lookup"><span data-stu-id="b88ae-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="b88ae-193">È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni file tooData Lake archiviati e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="b88ae-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="b88ae-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b88ae-194">See also</span></span>
* [<span data-ttu-id="b88ae-195">Portale di Azure: creare un toouse cluster HDInsight archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="b88ae-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
