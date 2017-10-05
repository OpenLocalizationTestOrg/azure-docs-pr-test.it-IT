---
title: Creare cluster HDInsight con Data Lake Store come risorsa di archiviazione predefinita usando PowerShell | Microsoft Docs
description: Usare Azure PowerShell per creare e usare cluster HDInsight con Azure Data Lake Store
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
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="8d3cb-103">Creare cluster HDInsight con Data Lake Store come risorsa di archiviazione predefinita usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d3cb-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d3cb-104">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8d3cb-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="8d3cb-105">Usare PowerShell (per l'archiviazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="8d3cb-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="8d3cb-106">Usare PowerShell (per l'archiviazione aggiuntiva)</span><span class="sxs-lookup"><span data-stu-id="8d3cb-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="8d3cb-107">Usare Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d3cb-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="8d3cb-108">Informazioni su come usare Azure PowerShell per configurare cluster Azure HDInsight con Azure Data Lake Store come risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="8d3cb-109">Per istruzioni su come creare un cluster HDInsight con Data Lake Store come risorsa di archiviazione aggiuntiva, vedere [Usare Azure PowerShell per creare un cluster HDInsight con Data Lake Store (come risorsa di archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="8d3cb-110">Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="8d3cb-111">L'opzione per creare cluster HDInsight con accesso a Data Lake Store come risorsa di archiviazione predefinita è disponibile per le versioni 3.5 e 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="8d3cb-112">L'opzione per creare cluster HDInsight con accesso a Data Lake Store come risorsa di archiviazione predefinita *non è disponibile* per i cluster HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="8d3cb-113">Per configurare HDInsight per il funzionamento con Data Lake Store usando PowerShell, seguire le istruzioni nelle cinque sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d3cb-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8d3cb-114">Prerequisites</span></span>
<span data-ttu-id="8d3cb-115">Prima di iniziare l'esercitazione, verificare di soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="8d3cb-116">**Sottoscrizione di Azure**: passare a [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8d3cb-117">**Azure PowerShell 1.0 o versione successiva**: vedere l'articolo su [come installare e configurare PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8d3cb-118">**Windows Software Development Kit (SDK)**: per installare Windows SDK, passare a [Download e strumenti per Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="8d3cb-119">L'SDK viene usato per creare un certificato di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="8d3cb-120">**Entità servizio Azure Active Directory**: questa esercitazione descrive come creare un'entità servizio in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8d3cb-121">Tuttavia, per creare un'entità servizio è necessario essere un amministratore di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="8d3cb-122">Se si è un amministratore, è possibile ignorare questo prerequisito e procedere con l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8d3cb-123">È possibile creare un'entità servizio solo se si è un amministratore di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="8d3cb-124">Prima di poter creare un cluster HDInsight con Data Lake Store, un amministratore di Azure AD deve creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="8d3cb-125">L'entità servizio deve essere creata con un certificato, come descritto in [Creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="8d3cb-126">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8d3cb-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="8d3cb-127">Per creare un account Data Lake Store, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="8d3cb-128">Sul desktop aprire una finestra di PowerShell e quindi immettere i frammenti di codice seguenti.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="8d3cb-129">Quando viene richiesto di effettuare l'accesso, accedere come amministratore o proprietario della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="8d3cb-130">Se si registra il provider di risorse Data Lake Store e viene visualizzato un errore simile a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, la sottoscrizione potrebbe non essere inclusa nell'elenco elementi consentiti per Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="8d3cb-131">Per abilitare la sottoscrizione di Azure per l'anteprima pubblica di Data Lake Store, seguire le istruzioni in [Introduzione all'uso di Azure Data Lake Store tramite il portale di Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="8d3cb-132">Un account Data Lake Store è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="8d3cb-133">Iniziare creando un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="8d3cb-134">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="8d3cb-135">Creare un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="8d3cb-136">Il nome dell'account specificato deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="8d3cb-137">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="8d3cb-138">Per usare Data Lake Store come risorsa di archiviazione predefinita, è necessario specificare un percorso radice in cui vengono copiati i file specifici del cluster durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="8d3cb-139">Per creare un percorso radice, che nel frammento di codice è **/cluster/hdiadlcluster**, usare i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="8d3cb-140">Configurare l'autenticazione per l'accesso basato sui ruoli all'Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8d3cb-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="8d3cb-141">Ogni sottoscrizione di Azure è associata a un'entità di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="8d3cb-142">Gli utenti e i servizi che accedono alle risorse della sottoscrizione usando il portale di Azure o l'API di Azure Resource Manager devono prima autenticarsi con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="8d3cb-143">L'accesso viene concesso alle sottoscrizioni e ai servizi di Azure tramite l'assegnazione del ruolo appropriato in una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="8d3cb-144">Per i servizi, un'entità servizio identifica il servizio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="8d3cb-145">Questa sezione illustra come concedere a un servizio dell'applicazione, ad esempio HDInsight, l'accesso a una risorsa di Azure, ovvero l'account Data Lake Store creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="8d3cb-146">A tale scopo, è necessario creare un'entità servizio per l'applicazione e assegnare ruoli a tale entità tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="8d3cb-147">Per configurare l'autenticazione di Active Directory per Azure Data Lake, eseguire le attività nelle due sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="8d3cb-148">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="8d3cb-148">Create a self-signed certificate</span></span>
<span data-ttu-id="8d3cb-149">Assicurarsi di avere installato [Windows SDK](https://dev.windows.com/en-us/downloads) prima di continuare con i passaggi descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="8d3cb-150">È necessario aver creato anche una directory, ad esempio *C:\mycertdir*, in cui creare il certificato.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="8d3cb-151">Dalla finestra di PowerShell passare al percorso in cui è installato Windows SDK, in genere *C:\Programmi (x86)\Windows Kits\10\bin\x86*, e usare l'utilità [MakeCert][makecert] per creare un certificato autofirmato e una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="8d3cb-152">Usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="8d3cb-153">Verrà richiesto di immettere la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="8d3cb-154">Una volta completata l'esecuzione del comando, nella directory del certificato specificata saranno presenti **CertFile.cer** e **mykey.pvk**.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="8d3cb-155">Usare l'utilità [Pvk2Pfx][pvk2pfx] per convertire i file con estensione PVK e CER creati da MakeCert in un file con estensione PFX.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="8d3cb-156">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="8d3cb-157">Quando viene chiesto, immettere la password della chiave privata specificata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="8d3cb-158">Il valore specificato per il parametro **-po** è la password associata al file PFX.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="8d3cb-159">Dopo il completamento del comando, nella directory del certificato specificata dovrebbe essere presente anche un file denominato **CertFile.pfx**.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="8d3cb-160">Creare un'applicazione Azure AD e un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="8d3cb-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="8d3cb-161">In questa sezione si crea un'entità servizio per un'applicazione Azure AD, si assegna un ruolo all'entità servizio e si esegue l'autenticazione come entità servizio fornendo un certificato.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="8d3cb-162">Per creare un'applicazione in Azure AD, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="8d3cb-163">Incollare i cmdlet seguenti nella finestra della console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="8d3cb-164">Assicurarsi che il valore specificato per la proprietà **-DisplayName** sia univoco.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="8d3cb-165">I valori per **-HomePage** e **-IdentiferUris** sono valori segnaposto e non vengono verificati.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="8d3cb-166">Creare un'entità servizio usando l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="8d3cb-167">Concedere l'accesso dell'entità servizio alla radice di Data Lake Store e a tutte le cartelle nel percorso radice specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="8d3cb-168">Usare i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="8d3cb-169">Creare un cluster HDInsight Linux con Data Lake Store come risorsa di archiviazione predefinita</span><span class="sxs-lookup"><span data-stu-id="8d3cb-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="8d3cb-170">In questa sezione viene creato un cluster HDInsight Hadoop Linux con Data Lake Store come risorsa di archiviazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="8d3cb-171">Per questa versione, il cluster HDInsight e Data Lake Store devono trovarsi nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="8d3cb-172">Recuperare l'ID tenant della sottoscrizione e archiviarlo per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="8d3cb-173">Creare il cluster HDInsight usando i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
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

    <span data-ttu-id="8d3cb-174">Dopo il completamento del cmdlet, dovrebbe viene visualizzato un output con i dettagli del cluster.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="8d3cb-175">Eseguire i processi di test sul cluster HDInsight per usare Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8d3cb-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="8d3cb-176">Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di test sul cluster per verificare che possa accedere a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="8d3cb-177">A tale scopo, eseguire un processo Hive di esempio che crea una tabella che usa i dati di esempio già disponibili in Data Lake Store in *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="8d3cb-178">In questa sezione si stabilisce una connessione SSH (Secure Shell) al cluster HDInsight Linux creato e quindi si esegue una query Hive di esempio.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="8d3cb-179">Se si usa un client Windows per stabilire una connessione SSH al cluster, vedere [Usare SSH con Hadoop basato su Linux in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="8d3cb-180">Se si usa un client Linux per stabilire una connessione SSH al cluster, vedere [Usare SSH con Hadoop basato su Linux in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="8d3cb-181">Dopo aver stabilito la connessione, avviare l'interfaccia della riga di comando di Hive usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="8d3cb-182">Usare l'interfaccia della riga di comando per immettere le istruzioni seguenti per creare una nuova tabella denominata **vehicles** con i dati di esempio in Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="8d3cb-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="8d3cb-183">L'output della query dovrebbe essere visualizzato nella console SSH.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8d3cb-184">Il percorso ai dati di esempio nel comando CREATE TABLE precedente è `adl:///example/data/`, dove `adl:///` è la radice del cluster.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="8d3cb-185">In base all'esempio della radice del cluster specificato in questa esercitazione, il comando è `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="8d3cb-186">È possibile usare l'alternativa più breve o indicare il percorso completo della radice del cluster.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="8d3cb-187">Accedere a Data Lake Store tramite comandi HDFS</span><span class="sxs-lookup"><span data-stu-id="8d3cb-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="8d3cb-188">Dopo aver configurato il cluster HDInsight per usare Data Lake Store, è possibile usare i comandi della shell HDFS (Hadoop Distributed File System) per accedere all'archivio.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="8d3cb-189">In questa sezione si stabilisce una connessione SSH al cluster HDInsight Linux creato e quindi si eseguono i comandi HDFS.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="8d3cb-190">Se si usa un client Windows per stabilire una connessione SSH al cluster, vedere [Usare SSH con Hadoop basato su Linux in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="8d3cb-191">Se si usa un client Linux per stabilire una connessione SSH al cluster, vedere [Usare SSH con Hadoop basato su Linux in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8d3cb-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="8d3cb-192">Dopo avere stabilito la connessione, elencare i file in Data Lake Store usando il comando del file system HDFS seguente.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="8d3cb-193">È anche possibile usare il comando `hdfs dfs -put` per caricare alcuni file in Data Lake Store e quindi usare `hdfs dfs -ls` per verificare se i file sono stati caricati correttamente.</span><span class="sxs-lookup"><span data-stu-id="8d3cb-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d3cb-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8d3cb-194">See also</span></span>
* [<span data-ttu-id="8d3cb-195">Portale di Azure: Creare un cluster HDInsight per usare Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8d3cb-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
