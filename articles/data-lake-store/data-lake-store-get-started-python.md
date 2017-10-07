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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Introduzione ad Azure Data Lake Store con Python

> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Informazioni su come toouse hello SDK Python per operazioni di base tooperform Azure e archivio Azure Data Lake, ad esempio creano cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Prerequisiti

* **Python**. È possibile scaricare Python [qui](https://www.python.org/downloads/). In questo articolo viene usata la versione 3.5.2 di Python.

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Creare un'applicazione di Azure Active Directory**. Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD. Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Installare i moduli di hello

toowork con archivio Data Lake usando Python, è necessario tooinstall tre moduli.

* Hello `azure-mgmt-resource` modulo. include i moduli Azure per Active Directory e così via.
* Hello `azure-mgmt-datalake-store` modulo. Sono incluse le operazioni di gestione account archivio Azure Data Lake hello. Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo di gestione di Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Hello `azure-datalake-store` modulo. Sono incluse le operazioni di filesystem hello archivio Azure Data Lake. Per altre informazioni su questo modulo, vedere la [documentazione di riferimento al modulo del file system di Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).

Utilizzare hello seguenti moduli hello tooinstall di comandi.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Creare una nuova applicazione Python

1. Nell'IDE di propria scelta hello, ad esempio, creare una nuova applicazione Python, **mysample.py**.

2. Aggiungere hello seguenti moduli hello necessario tooimport di righe

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

3. Salvare le modifiche toomysample.py.

## <a name="authentication"></a>Autenticazione

In questa sezione, si parlerà hello modi tooauthenticate con Azure AD. Hello opzioni disponibili sono:

* Autenticazione dell'utente finale
* Autenticazione da servizio a servizio
* Autenticazione a più fattori

È necessario usare queste opzioni di autenticazione per i moduli di gestione degli account e di gestione del file system.

### <a name="end-user-authentication-for-account-management"></a>Autenticazione dell'utente finale per la gestione degli account

Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.). È necessario specificare il nome utente e la password per un utente di Azure AD. Si noti che l'utente hello non deve essere configurato per l'autenticazione a più fattori.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Autenticazione dell'utente finale per le operazioni del file system

Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via). Usare questo tipo di autenticazione con un'applicazione **client nativa** di Azure AD. utente Hello Azure AD per che fornire le credenziali non deve essere configurati per l'autenticazione a più fattori.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Autenticazione da servizio a servizio con segreto client per la gestione degli account

Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.). Hello seguente frammento di codice può essere utilizzato tooauthenticate l'applicazione in modo non interattivo, utilizzando la chiave privata client hello per un'entità applicazione / servizio. Usare questo frammento con un'app Web di Azure AD esistente.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Autenticazione da servizio a servizio con segreto client per le operazioni del file system

Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via). Hello seguente frammento di codice può essere utilizzato tooauthenticate l'applicazione in modo non interattivo, utilizzando la chiave privata client hello per un'entità applicazione / servizio. Usare questo frammento con un'app Web di Azure AD esistente.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Multi-Factor Authentication per la gestione degli account

Utilizzare questo tooauthenticate con Azure AD per operazioni di gestione di account (creazione/eliminazione account archivio Data Lake, ecc.). Hello frammento di codice seguente può essere utilizzato tooauthenticate l'applicazione utilizza l'autenticazione a più fattori. Usare questo frammento con un'app Web di Azure AD esistente.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Multi-Factor Authentication per la gestione del file system

Utilizzare questo tooauthenticate con Azure AD per le operazioni di file System (Crea cartella file di caricamento, e così via). Hello frammento di codice seguente può essere utilizzato tooauthenticate l'applicazione utilizza l'autenticazione a più fattori. Usare questo frammento con un'app Web di Azure AD esistente.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Creare un gruppo di risorse di Azure

Utilizzare hello seguente frammento di codice toocreate un gruppo di risorse di Azure:

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

## <a name="create-clients-and-data-lake-store-account"></a>Creare client e account Data Lake Store

Hello seguente frammento di codice prima crea client account archivio Data Lake di hello. Usa hello client oggetto toocreate un account archivio Data Lake. Infine, hello frammento consente di creare un oggetto client di file System.

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

## <a name="list-hello-data-lake-store-accounts"></a>Elenco di account archivio Data Lake hello

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Creare una directory

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Caricare un file


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Scaricare un file

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Eliminare una directory

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Vedere anche

- [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
- [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Usare Azure HDInsight con Archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Informazioni di riferimento su .NET SDK con Data Lake Store](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
