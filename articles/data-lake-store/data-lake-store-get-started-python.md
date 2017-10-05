---
title: Usare Python SDK per iniziare a usare Azure Data Lake Store | Documentazione Microsoft
description: Informazioni su come usare Python SDK insieme agli account Data Lake Store e al file system.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="20593-103">Introduzione ad Azure Data Lake Store con Python</span><span class="sxs-lookup"><span data-stu-id="20593-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20593-104">Portale</span><span class="sxs-lookup"><span data-stu-id="20593-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="20593-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20593-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="20593-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="20593-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="20593-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="20593-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="20593-108">API REST</span><span class="sxs-lookup"><span data-stu-id="20593-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="20593-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="20593-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="20593-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="20593-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="20593-111">Python</span><span class="sxs-lookup"><span data-stu-id="20593-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="20593-112">Informazioni su come usare Python SDK per Azure e Azure Data Lake Store per eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20593-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20593-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20593-113">Prerequisites</span></span>

* <span data-ttu-id="20593-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="20593-114">**Python**.</span></span> <span data-ttu-id="20593-115">È possibile scaricare Python [qui](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="20593-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="20593-116">In questo articolo viene usata la versione 3.5.2 di Python.</span><span class="sxs-lookup"><span data-stu-id="20593-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="20593-117">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="20593-117">**An Azure subscription**.</span></span> <span data-ttu-id="20593-118">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20593-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="20593-119">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20593-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="20593-120">Usare l'applicazione Azure AD per autenticare l'applicazione Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="20593-121">Per l'autenticazione con Azure AD è possibile usare l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="20593-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="20593-122">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="20593-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="20593-123">Installare i moduli</span><span class="sxs-lookup"><span data-stu-id="20593-123">Install the modules</span></span>

<span data-ttu-id="20593-124">Per gestire Data Lake Store usando Python, è necessario installare tre moduli.</span><span class="sxs-lookup"><span data-stu-id="20593-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="20593-125">Il modulo `azure-mgmt-resource`</span><span class="sxs-lookup"><span data-stu-id="20593-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="20593-126">include i moduli Azure per Active Directory e così via.</span><span class="sxs-lookup"><span data-stu-id="20593-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="20593-127">Il modulo `azure-mgmt-datalake-store`</span><span class="sxs-lookup"><span data-stu-id="20593-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="20593-128">include le operazioni di gestione account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="20593-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="20593-129">Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo di gestione di Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="20593-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="20593-130">Il modulo `azure-datalake-store`</span><span class="sxs-lookup"><span data-stu-id="20593-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="20593-131">include le operazioni del file system di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="20593-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="20593-132">Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo del file system di Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="20593-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="20593-133">Per installare i moduli, usare i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="20593-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="20593-134">Creare una nuova applicazione Python</span><span class="sxs-lookup"><span data-stu-id="20593-134">Create a new Python application</span></span>

1. <span data-ttu-id="20593-135">In un IDE a scelta creare una nuova applicazione Python, ad esempio **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="20593-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="20593-136">Aggiungere le righe seguenti per importare i moduli necessari</span><span class="sxs-lookup"><span data-stu-id="20593-136">Add the following lines to import the required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="20593-137">Salvare le modifiche a mysample.py.</span><span class="sxs-lookup"><span data-stu-id="20593-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="20593-138">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="20593-138">Authentication</span></span>

<span data-ttu-id="20593-139">Questa sezione descrive le diverse modalità di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="20593-140">Le opzioni disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="20593-140">The options available are:</span></span>

* <span data-ttu-id="20593-141">Autenticazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="20593-141">End-user authentication</span></span>
* <span data-ttu-id="20593-142">Autenticazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="20593-142">Service-to-service authentication</span></span>
* <span data-ttu-id="20593-143">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="20593-143">Multi-factor authentication</span></span>

<span data-ttu-id="20593-144">È necessario usare queste opzioni di autenticazione per i moduli di gestione degli account e di gestione del file system.</span><span class="sxs-lookup"><span data-stu-id="20593-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="20593-145">Autenticazione dell'utente finale per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="20593-145">End-user authentication for account management</span></span>

<span data-ttu-id="20593-146">Per le operazioni di gestione degli account, ad esempio creare o eliminare account Data Lake Store e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="20593-147">È necessario specificare il nome utente e la password per un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="20593-148">L'utente non deve essere configurato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="20593-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="20593-149">Autenticazione dell'utente finale per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="20593-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="20593-150">Per le operazioni di gestione del file system, ad esempio creare cartelle, caricare file e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="20593-151">Usare questo tipo di autenticazione con un'applicazione **client nativa** di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="20593-152">L'utente AD Azure del quale sono state specificate le credenziali non deve essere configurato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="20593-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="20593-153">Autenticazione da servizio a servizio con segreto client per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="20593-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="20593-154">Per le operazioni di gestione degli account, ad esempio creare o eliminare account Data Lake Store e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="20593-155">Il frammento di codice seguente può essere usato per autenticare l'applicazione in modo non interattivo, usando il segreto client per un'applicazione o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="20593-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="20593-156">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="20593-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="20593-157">Autenticazione da servizio a servizio con segreto client per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="20593-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="20593-158">Per le operazioni di gestione del file system, ad esempio creare cartelle, caricare file e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="20593-159">Il frammento di codice seguente può essere usato per autenticare l'applicazione in modo non interattivo, usando il segreto client per un'applicazione o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="20593-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="20593-160">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="20593-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="20593-161">Multi-Factor Authentication per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="20593-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="20593-162">Per le operazioni di gestione degli account, ad esempio creare o eliminare account Data Lake Store e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="20593-163">Il frammento di codice seguente consente di autenticare l'applicazione con Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="20593-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="20593-164">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="20593-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="20593-165">Multi-Factor Authentication per la gestione del file system</span><span class="sxs-lookup"><span data-stu-id="20593-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="20593-166">Per le operazioni di gestione del file system, ad esempio creare cartelle, caricare file e così via, è necessario eseguire questo tipo di autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20593-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="20593-167">Il frammento di codice seguente consente di autenticare l'applicazione con Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="20593-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="20593-168">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="20593-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="20593-169">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="20593-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="20593-170">Per creare un gruppo di risorse di Azure usare il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="20593-170">Use the following code snippet to create an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="20593-171">Creare client e account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="20593-172">Il frammento seguente crea prima il client account Data Lake Store,</span><span class="sxs-lookup"><span data-stu-id="20593-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="20593-173">poi usa l'oggetto client per creare un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="20593-174">e infine crea un oggetto client per il file system.</span><span class="sxs-lookup"><span data-stu-id="20593-174">Finally, the snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="20593-175">Elencare gli account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="20593-176">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="20593-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="20593-177">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="20593-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="20593-178">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="20593-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="20593-179">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="20593-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="20593-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="20593-180">See also</span></span>

- [<span data-ttu-id="20593-181">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="20593-182">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="20593-183">Usare Azure HDInsight con Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="20593-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="20593-184">Informazioni di riferimento su .NET SDK con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20593-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="20593-185">Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="20593-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
