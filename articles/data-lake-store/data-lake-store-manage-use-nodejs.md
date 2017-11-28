---
title: aaaGet avviato con l'archivio Azure Data Lake con Azure SDK per Node.js | Documenti Microsoft
description: Informazioni su come toouse Node.js toowork con account archivio Data Lake e hello del file system.
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="70a9d-103">Introduzione ad Azure Data Lake Store con Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="70a9d-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70a9d-104">Portale</span><span class="sxs-lookup"><span data-stu-id="70a9d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="70a9d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70a9d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="70a9d-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="70a9d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="70a9d-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="70a9d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="70a9d-108">API REST</span><span class="sxs-lookup"><span data-stu-id="70a9d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="70a9d-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="70a9d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="70a9d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="70a9d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="70a9d-111">Python</span><span class="sxs-lookup"><span data-stu-id="70a9d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="70a9d-112">Per caricare e scaricare grandi quantità di dati (file di grandi dimensioni, un numero elevato di file o entrambi), è consigliabile utilizzare hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI di Azure 2.0](data-lake-store-get-started-cli-2.0.md), o [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="70a9d-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="70a9d-113">Queste opzioni offrono prestazioni migliori perché usano lo spostamento dati di più thread tooparallelize hello.</span><span class="sxs-lookup"><span data-stu-id="70a9d-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="70a9d-114">Informazioni su come toouse hello Azure SDK per Node.js toocreate un account archivio Azure Data Lake ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70a9d-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="70a9d-115">Attualmente, hello SDK supporta</span><span class="sxs-lookup"><span data-stu-id="70a9d-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="70a9d-116">**Versione di Node.js: 0.10.0 o successiva**</span><span class="sxs-lookup"><span data-stu-id="70a9d-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="70a9d-117">**Versione dell'API REST per l'account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="70a9d-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="70a9d-118">**Versione dell'API REST per FileSystem: 2015-10-01-anteprima**</span><span class="sxs-lookup"><span data-stu-id="70a9d-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70a9d-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="70a9d-119">Prerequisites</span></span>
<span data-ttu-id="70a9d-120">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="70a9d-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="70a9d-121">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="70a9d-121">**An Azure subscription**.</span></span> <span data-ttu-id="70a9d-122">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70a9d-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="70a9d-123">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70a9d-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="70a9d-124">Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a9d-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="70a9d-125">Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="70a9d-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="70a9d-126">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="70a9d-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="70a9d-127">Come tooInstall</span><span class="sxs-lookup"><span data-stu-id="70a9d-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="70a9d-128">Eseguire l'autenticazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70a9d-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="70a9d-129">Hello i frammenti di codice seguente mostra due modi diversi di autenticazione con l'archivio Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a9d-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="70a9d-130">Per informazioni dettagliate su toouse metodi diversi per l'autenticazione con l'archivio Data Lake, vedere [autentica con archivio Data Lake tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="70a9d-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="70a9d-131">frammento di Hello seguente richiede l'input come nome di dominio Azure AD, ID client per un'app di Azure AD e così via. Tutti questi dettagli possono essere recuperati da un'applicazione Azure AD che è necessario creata, hello cui dettagli sono inoltre inclusi nel collegamento riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="70a9d-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="70a9d-132">Creare i client di archivio hello Data Lake</span><span class="sxs-lookup"><span data-stu-id="70a9d-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="70a9d-133">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="70a9d-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="70a9d-134">Creare un file con contenuto</span><span class="sxs-lookup"><span data-stu-id="70a9d-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="70a9d-135">Ottenere un elenco di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="70a9d-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="70a9d-136">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="70a9d-136">See also</span></span>
* [<span data-ttu-id="70a9d-137">Microsoft Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="70a9d-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="70a9d-138">Microsoft Azure SDK per Node. js - Gestione di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="70a9d-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

