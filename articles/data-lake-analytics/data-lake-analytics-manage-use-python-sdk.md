---
title: Gestire Azure Data Lake Analytics con Python | Microsoft Docs
description: 'Informazioni su come usare Python per creare un account di Data Lake Store e inviare i processi. '
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 31326a32f8748e6cfb8bfe24cda46c511ab59352
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="869cc-103">Gestire Azure Data Lake Analytics con Python</span><span class="sxs-lookup"><span data-stu-id="869cc-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="869cc-104">Versioni di Python</span><span class="sxs-lookup"><span data-stu-id="869cc-104">Python versions</span></span>

* <span data-ttu-id="869cc-105">Usare una versione a 64 bit di Python.</span><span class="sxs-lookup"><span data-stu-id="869cc-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="869cc-106">È possibile usare la distribuzione di Python standard disponibile in **[Python.org downloads](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="869cc-106">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="869cc-107">Molti sviluppatori trovano utile usare la **[distribuzione Anaconda Python](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="869cc-107">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="869cc-108">Questo articolo si basa su Python versione 3.6 della distribuzione di Python standard</span><span class="sxs-lookup"><span data-stu-id="869cc-108">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="869cc-109">Installare Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="869cc-109">Install Azure Python SDK</span></span>

<span data-ttu-id="869cc-110">Installare i moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="869cc-110">Install the following modules:</span></span>

* <span data-ttu-id="869cc-111">Il modulo **azure-mgmt-resource** include altri moduli di Azure per Active Directory e così via.</span><span class="sxs-lookup"><span data-stu-id="869cc-111">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="869cc-112">Il modulo **azure-mgmt-datalake-store** include le operazioni di gestione account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="869cc-112">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="869cc-113">Il modulo **azure-datalake-store** include le operazioni di file system di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="869cc-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="869cc-114">Il modulo **azure-datalake-analytics** include le operazioni di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="869cc-114">The **azure-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="869cc-115">Assicurarsi prima di tutto di avere la versione più recente di `pip` usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="869cc-115">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="869cc-116">Questo documento si basa su `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="869cc-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="869cc-117">Per installare i moduli dalla riga di comando, usare i comandi `pip` seguenti:</span><span class="sxs-lookup"><span data-stu-id="869cc-117">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="869cc-118">Creare un nuovo script Python</span><span class="sxs-lookup"><span data-stu-id="869cc-118">Create a new Python script</span></span>

<span data-ttu-id="869cc-119">Incollare il codice seguente nello script:</span><span class="sxs-lookup"><span data-stu-id="869cc-119">Paste the following code into the script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="869cc-120">Eseguire questo script per verificare che i moduli possano essere importati.</span><span class="sxs-lookup"><span data-stu-id="869cc-120">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="869cc-121">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="869cc-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="869cc-122">Autenticazione utente interattiva con un popup</span><span class="sxs-lookup"><span data-stu-id="869cc-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="869cc-123">Questo metodo non è supportato.</span><span class="sxs-lookup"><span data-stu-id="869cc-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="869cc-124">Autenticazione utente interattiva con un codice di dispositivo</span><span class="sxs-lookup"><span data-stu-id="869cc-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="869cc-125">Autenticazione non interattiva con una SPI e un segreto</span><span class="sxs-lookup"><span data-stu-id="869cc-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="869cc-126">Autenticazione non interattiva con un'API e un certificato</span><span class="sxs-lookup"><span data-stu-id="869cc-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="869cc-127">Questo metodo non è supportato.</span><span class="sxs-lookup"><span data-stu-id="869cc-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="869cc-128">Variabili dello script comuni</span><span class="sxs-lookup"><span data-stu-id="869cc-128">Common script variables</span></span>

<span data-ttu-id="869cc-129">Negli esempi sono usate queste variabili.</span><span class="sxs-lookup"><span data-stu-id="869cc-129">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="869cc-130">Creare i client</span><span class="sxs-lookup"><span data-stu-id="869cc-130">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="869cc-131">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="869cc-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="869cc-132">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="869cc-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="869cc-133">Creare prima un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="869cc-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="869cc-134">Creare quindi un account ADLA che usa tale archivio.</span><span class="sxs-lookup"><span data-stu-id="869cc-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="869cc-135">Inviare un processo</span><span class="sxs-lookup"><span data-stu-id="869cc-135">Submit a job</span></span>

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="869cc-136">Attendere la fine di un processo</span><span class="sxs-lookup"><span data-stu-id="869cc-136">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="869cc-137">Elencare pipeline e ricorrenze</span><span class="sxs-lookup"><span data-stu-id="869cc-137">List pipelines and recurrences</span></span>
<span data-ttu-id="869cc-138">A seconda se i processi hanno pipeline o metadati associati, è possibile elencare le pipeline e le ricorrenze.</span><span class="sxs-lookup"><span data-stu-id="869cc-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="869cc-139">Gestire i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="869cc-139">Manage compute policies</span></span>

<span data-ttu-id="869cc-140">L'oggetto DataLakeAnalyticsAccountManagementClient offre metodi per gestire i criteri di calcolo per un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="869cc-140">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="869cc-141">Elencare i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="869cc-141">List compute policies</span></span>

<span data-ttu-id="869cc-142">Il codice seguente recupera un elenco di criteri di calcolo per un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="869cc-142">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="869cc-143">Creare un nuovo criterio di calcolo</span><span class="sxs-lookup"><span data-stu-id="869cc-143">Create a new compute policy</span></span>

<span data-ttu-id="869cc-144">Il codice seguente crea un nuovo criterio di calcolo per un account Data Lake Analytics, impostando il massimo di unità di analisi disponibile per l'utente specificato su 50 e la priorità minima del processo su 250.</span><span class="sxs-lookup"><span data-stu-id="869cc-144">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="869cc-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="869cc-145">Next steps</span></span>

- <span data-ttu-id="869cc-146">Per visualizzare la stessa esercitazione usando altri strumenti, scegliere i selettori di scheda nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="869cc-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="869cc-147">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="869cc-147">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="869cc-148">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="869cc-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

