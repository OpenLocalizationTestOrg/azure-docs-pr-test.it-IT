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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Introduzione ad Azure Data Lake Store con Azure SDK per Node.js
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

> [!NOTE]
> Per caricare e scaricare grandi quantità di dati (file di grandi dimensioni, un numero elevato di file o entrambi), è consigliabile utilizzare hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI di Azure 2.0](data-lake-store-get-started-cli-2.0.md), o [Azure PowerShell](data-lake-store-get-started-powershell.md). Queste opzioni offrono prestazioni migliori perché usano lo spostamento dati di più thread tooparallelize hello.
> 
> 

Informazioni su come toouse hello Azure SDK per Node.js toocreate un account archivio Azure Data Lake ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md). Attualmente, hello SDK supporta

* **Versione di Node.js: 0.10.0 o successiva**
* **Versione dell'API REST per l'account: 2015-10-01-preview**
* **Versione dell'API REST per FileSystem: 2015-10-01-anteprima**

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Creare un'applicazione di Azure Active Directory**. Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD. Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Come tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Eseguire l'autenticazione con Azure Active Directory
Hello i frammenti di codice seguente mostra due modi diversi di autenticazione con l'archivio Data Lake con Azure AD. Per informazioni dettagliate su toouse metodi diversi per l'autenticazione con l'archivio Data Lake, vedere [autentica con archivio Data Lake tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

frammento di Hello seguente richiede l'input come nome di dominio Azure AD, ID client per un'app di Azure AD e così via. Tutti questi dettagli possono essere recuperati da un'applicazione Azure AD che è necessario creata, hello cui dettagli sono inoltre inclusi nel collegamento riportato sopra.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Creare i client di archivio hello Data Lake
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Creare un account Archivio Data Lake
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

## <a name="create-a-file-with-content"></a>Creare un file con contenuto
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

## <a name="get-a-list-of-files-and-folders"></a>Ottenere un elenco di file e cartelle
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

## <a name="see-also"></a>Vedere anche
* [Microsoft Azure SDK per Node.js](https://github.com/azure/azure-sdk-for-node)
* [Microsoft Azure SDK per Node. js - Gestione di Analisi Data Lake](https://www.npmjs.com/package/azure-arm-datalake-analytics)

