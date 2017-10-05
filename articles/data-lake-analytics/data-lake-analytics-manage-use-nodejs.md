---
title: Gestire Azure Data Lake Analytics con Azure SDK per Node.js | Documentazione Microsoft
description: Informazioni su come gestire gli account, le origini dati, i processi e gli utenti di Data Lake Analytics tramite Azure SDK per Node.js
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 769cf9b09eecd204c8b5b944065dad57a6d73231
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="9ecb0-103">Gestire Azure Data Lake Analytics tramite Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="9ecb0-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="9ecb0-104">Azure SDK per Node. js può essere usato per gestire account, processi e cataloghi di Analisi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9ecb0-104">The Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="9ecb0-105">Per visualizzare l'argomento relativo alla gestione tramite altri strumenti, fare clic sul selettore di scheda riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="9ecb0-105">To see management topic using other tools, click the tab select above.</span></span>

<span data-ttu-id="9ecb0-106">Attualmente supporta:</span><span class="sxs-lookup"><span data-stu-id="9ecb0-106">Right now it supports:</span></span>

* <span data-ttu-id="9ecb0-107">**Versione di Node.js: 0.10.0 o successiva**</span><span class="sxs-lookup"><span data-stu-id="9ecb0-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="9ecb0-108">**Versione dell'API REST per l'account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9ecb0-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9ecb0-109">**Versione dell'API REST per il catalogo: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9ecb0-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9ecb0-110">**Versione dell'API REST per il processo: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="9ecb0-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="9ecb0-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="9ecb0-111">Features</span></span>
* <span data-ttu-id="9ecb0-112">Gestione account: creare, ottenere, elencare, aggiornare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="9ecb0-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="9ecb0-113">Gestione dei processi: inviare, ottenere, elencare, annullare.</span><span class="sxs-lookup"><span data-stu-id="9ecb0-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="9ecb0-114">Gestione del catalogo: ottenere ed elencare.</span><span class="sxs-lookup"><span data-stu-id="9ecb0-114">Catalog management: get and list.</span></span>

## <a name="how-to-install"></a><span data-ttu-id="9ecb0-115">Come eseguire l'installazione</span><span class="sxs-lookup"><span data-stu-id="9ecb0-115">How to Install</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="9ecb0-116">Eseguire l'autenticazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ecb0-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-analytics-client"></a><span data-ttu-id="9ecb0-117">Creare il client di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="9ecb0-117">Create the Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="9ecb0-118">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="9ecb0-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created to create
// a Data Lake Analytics account. See the Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="9ecb0-119">Ottenere un elenco di processi</span><span class="sxs-lookup"><span data-stu-id="9ecb0-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-the-data-lake-analytics-catalog"></a><span data-ttu-id="9ecb0-120">Ottenere un elenco di database nel catalogo di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="9ecb0-120">Get a list of databases in the Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="9ecb0-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9ecb0-121">See also</span></span>
* [<span data-ttu-id="9ecb0-122">Microsoft Azure SDK per Node.js</span><span class="sxs-lookup"><span data-stu-id="9ecb0-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="9ecb0-123">Microsoft Azure SDK per Node. js - Gestione dell'Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="9ecb0-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

