---
title: aaaUse hello Python SDK tooget avviato con l'archivio Azure Data Lake | Documenti Microsoft
description: Informazioni su come toouse Python SDK toowork con account archivio Data Lake e hello del file system.
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
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="24748-103">Introduzione ad Azure Data Lake Store con Python</span><span class="sxs-lookup"><span data-stu-id="24748-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24748-104">Portale</span><span class="sxs-lookup"><span data-stu-id="24748-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="24748-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24748-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="24748-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="24748-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="24748-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="24748-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="24748-108">API REST</span><span class="sxs-lookup"><span data-stu-id="24748-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="24748-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="24748-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="24748-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="24748-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="24748-111">Python</span><span class="sxs-lookup"><span data-stu-id="24748-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="24748-112">Informazioni su come toouse hello SDK Python per operazioni di base tooperform Azure e archivio Azure Data Lake, ad esempio creano cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24748-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24748-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="24748-113">Prerequisites</span></span>

* <span data-ttu-id="24748-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="24748-114">**Python**.</span></span> <span data-ttu-id="24748-115">È possibile scaricare Python [qui](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="24748-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="24748-116">In questo articolo viene usata la versione 3.5.2 di Python.</span><span class="sxs-lookup"><span data-stu-id="24748-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="24748-117">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="24748-117">**An Azure subscription**.</span></span> <span data-ttu-id="24748-118">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24748-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="24748-119">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24748-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="24748-120">Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24748-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="24748-121">Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="24748-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="24748-122">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="24748-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="24748-123">Installare i moduli di hello</span><span class="sxs-lookup"><span data-stu-id="24748-123">Install hello modules</span></span>

<span data-ttu-id="24748-124">toowork con archivio Data Lake usando Python, è necessario tooinstall tre moduli.</span><span class="sxs-lookup"><span data-stu-id="24748-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="24748-125">Hello `azure-mgmt-resource` modulo.</span><span class="sxs-lookup"><span data-stu-id="24748-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="24748-126">include i moduli Azure per Active Directory e così via.</span><span class="sxs-lookup"><span data-stu-id="24748-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="24748-127">Hello `azure-mgmt-datalake-store` modulo.</span><span class="sxs-lookup"><span data-stu-id="24748-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="24748-128">Sono incluse le operazioni di gestione account archivio Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="24748-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="24748-129">Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo di gestione di Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="24748-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="24748-130">Hello `azure-datalake-store` modulo.</span><span class="sxs-lookup"><span data-stu-id="24748-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="24748-131">Sono incluse le operazioni di filesystem hello archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24748-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="24748-132">Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo del file system di Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="24748-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="24748-133">Utilizzare hello seguenti moduli hello tooinstall di comandi.</span><span class="sxs-lookup"><span data-stu-id="24748-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="24748-134">Creare una nuova applicazione Python</span><span class="sxs-lookup"><span data-stu-id="24748-134">Create a new Python application</span></span>

1. <span data-ttu-id="24748-135">Nell'IDE di propria scelta hello, ad esempio, creare una nuova applicazione Python, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="24748-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="24748-136">Aggiungere hello seguenti moduli hello necessario tooimport di righe</span><span class="sxs-lookup"><span data-stu-id="24748-136">Add hello following lines tooimport hello required modules</span></span>

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

3. <span data-ttu-id="24748-137">Salvare le modifiche toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="24748-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="24748-138">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="24748-138">Authentication</span></span>

<span data-ttu-id="24748-139">In questa sezione, si parlerà hello modi tooauthenticate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24748-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="24748-140">Hello opzioni disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="24748-140">hello options available are:</span></span>

* <span data-ttu-id="24748-141">Autenticazione dell'utente finale</span><span class="sxs-lookup"><span data-stu-id="24748-141">End-user authentication</span></span>
* <span data-ttu-id="24748-142">Autenticazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="24748-142">Service-to-service authentication</span></span>
* <span data-ttu-id="24748-143">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="24748-143">Multi-factor authentication</span></span>

<span data-ttu-id="24748-144">È necessario usare queste opzioni di autenticazione per i moduli di gestione degli account e di gestione del file system.</span><span class="sxs-lookup"><span data-stu-id="24748-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="24748-145">Autenticazione dell'utente finale per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="24748-145">End-user authentication for account management</span></span>

<span data-ttu-id="24748-146">Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.).</span><span class="sxs-lookup"><span data-stu-id="24748-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="24748-147">È necessario specificare il nome utente e la password per un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24748-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="24748-148">Si noti che l'utente hello non deve essere configurato per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="24748-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="24748-149">Autenticazione dell'utente finale per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="24748-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="24748-150">Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via).</span><span class="sxs-lookup"><span data-stu-id="24748-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="24748-151">Usare questo tipo di autenticazione con un'applicazione **client nativa** di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24748-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="24748-152">utente Hello Azure AD per che fornire le credenziali non deve essere configurati per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="24748-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="24748-153">Autenticazione da servizio a servizio con segreto client per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="24748-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="24748-154">Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.).</span><span class="sxs-lookup"><span data-stu-id="24748-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="24748-155">Hello seguente frammento di codice può essere utilizzato tooauthenticate l'applicazione in modo non interattivo, utilizzando la chiave privata client hello per un'entità applicazione / servizio.</span><span class="sxs-lookup"><span data-stu-id="24748-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="24748-156">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="24748-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="24748-157">Autenticazione da servizio a servizio con segreto client per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="24748-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="24748-158">Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via).</span><span class="sxs-lookup"><span data-stu-id="24748-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="24748-159">Hello seguente frammento di codice può essere utilizzato tooauthenticate l'applicazione in modo non interattivo, utilizzando la chiave privata client hello per un'entità applicazione / servizio.</span><span class="sxs-lookup"><span data-stu-id="24748-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="24748-160">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="24748-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="24748-161">Multi-Factor Authentication per la gestione degli account</span><span class="sxs-lookup"><span data-stu-id="24748-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="24748-162">Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.).</span><span class="sxs-lookup"><span data-stu-id="24748-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="24748-163">Hello frammento di codice seguente può essere utilizzato tooauthenticate l'applicazione utilizza l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="24748-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="24748-164">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="24748-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="24748-165">Multi-Factor Authentication per la gestione del file system</span><span class="sxs-lookup"><span data-stu-id="24748-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="24748-166">Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via).</span><span class="sxs-lookup"><span data-stu-id="24748-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="24748-167">Hello frammento di codice seguente può essere utilizzato tooauthenticate l'applicazione utilizza l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="24748-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="24748-168">Usare questo frammento con un'app Web di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="24748-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="24748-169">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="24748-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="24748-170">Utilizzare hello seguente frammento di codice toocreate un gruppo di risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="24748-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="24748-171">Creare client e account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="24748-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="24748-172">Hello seguente frammento di codice prima crea client account archivio Data Lake di hello.</span><span class="sxs-lookup"><span data-stu-id="24748-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="24748-173">Usa hello client oggetto toocreate un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24748-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="24748-174">Infine, hello frammento consente di creare un oggetto client di file System.</span><span class="sxs-lookup"><span data-stu-id="24748-174">Finally, hello snippet creates a filesystem client object.</span></span>

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

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="24748-175">Elenco di account archivio Data Lake hello</span><span class="sxs-lookup"><span data-stu-id="24748-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="24748-176">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="24748-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="24748-177">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="24748-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="24748-178">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="24748-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="24748-179">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="24748-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="24748-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="24748-180">See also</span></span>

- [<span data-ttu-id="24748-181">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="24748-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="24748-182">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="24748-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="24748-183">Usare Azure HDInsight con Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="24748-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="24748-184">Informazioni di riferimento su .NET SDK con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="24748-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="24748-185">Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="24748-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
