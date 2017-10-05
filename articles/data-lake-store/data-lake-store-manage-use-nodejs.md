---
title: Introduzione ad Azure Data Lake Store con Azure SDK per Node.js |Documentazione Microsoft
description: Informazioni su come usare Node.js con gli account Data Lake Store e il file system.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="01341-103">Introduzione ad Azure Data Lake Store con Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="01341-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01341-104">Portale</span><span class="sxs-lookup"><span data-stu-id="01341-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="01341-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01341-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="01341-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="01341-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="01341-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="01341-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="01341-108">API REST</span><span class="sxs-lookup"><span data-stu-id="01341-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="01341-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="01341-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="01341-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="01341-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="01341-111">Python</span><span class="sxs-lookup"><span data-stu-id="01341-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="01341-112">Per caricare e scaricare grandi quantità di dati (file di grandi dimensioni, un gran numero di file o entrambi), è consigliabile usare [Python SDK](data-lake-store-get-started-python.md), [.NET SDK](data-lake-store-get-started-net-sdk.md), [l'interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md) o [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="01341-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="01341-113">Queste opzioni offrono prestazioni migliori, perché usano più thread per parallelizzare lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="01341-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="01341-114">Informazioni su come usare Azure SDK per Node.js per creare un account Azure Data Lake Store ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare i file di dati, eliminare l'account e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01341-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="01341-115">L'SDK attualmente supporta:</span><span class="sxs-lookup"><span data-stu-id="01341-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="01341-116">**Versione di Node.js: 0.10.0 o successiva**</span><span class="sxs-lookup"><span data-stu-id="01341-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="01341-117">**Versione dell'API REST per l'account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="01341-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="01341-118">**Versione dell'API REST per FileSystem: 2015-10-01-anteprima**</span><span class="sxs-lookup"><span data-stu-id="01341-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01341-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="01341-119">Prerequisites</span></span>
<span data-ttu-id="01341-120">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="01341-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="01341-121">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="01341-121">**An Azure subscription**.</span></span> <span data-ttu-id="01341-122">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01341-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="01341-123">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01341-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="01341-124">Usare l'applicazione Azure AD per autenticare l'applicazione Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01341-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="01341-125">Per l'autenticazione con Azure AD è possibile usare l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="01341-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="01341-126">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="01341-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="01341-127">Come eseguire l'installazione</span><span class="sxs-lookup"><span data-stu-id="01341-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="01341-128">Eseguire l'autenticazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01341-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="01341-129">I frammenti seguenti illustrano due modi diversi per eseguire l'autenticazione con Data Lake Store usando Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01341-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="01341-130">Per una spiegazione dettagliata dei diversi metodi da usare per eseguire l'autenticazione con Data Lake Store, vedere [Eseguire l'autenticazione con Data Lake Store usando Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="01341-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="01341-131">Il frammento seguente richiede anche input come il nome di dominio di Azure AD, l'ID client per un'app Azure AD e così via. Tutti questi dettagli possono essere recuperati da un'applicazione Azure AD che è necessario creare. Per informazioni dettagliate, fare clic sul collegamento precedente.</span><span class="sxs-lookup"><span data-stu-id="01341-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="01341-132">Creare i client Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="01341-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="01341-133">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="01341-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="01341-134">Creare un file con contenuto</span><span class="sxs-lookup"><span data-stu-id="01341-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="01341-135">Ottenere un elenco di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="01341-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="01341-136">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="01341-136">See also</span></span>
* [<span data-ttu-id="01341-137">Microsoft Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="01341-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="01341-138">Microsoft Azure SDK per Node. js - Gestione di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="01341-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

