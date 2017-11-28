---
title: Azure Data Lake Analitica aaaManage usando Python | Documenti Microsoft
description: "Informazioni sulla modalità di memorizzazione una Data Lake di toouse Python toocreate account e inviare i processi. "
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
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="69dda-103">Gestire Azure Data Lake Analytics con Python</span><span class="sxs-lookup"><span data-stu-id="69dda-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="69dda-104">Versioni di Python</span><span class="sxs-lookup"><span data-stu-id="69dda-104">Python versions</span></span>

* <span data-ttu-id="69dda-105">Usare una versione a 64 bit di Python.</span><span class="sxs-lookup"><span data-stu-id="69dda-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="69dda-106">È possibile utilizzare distribuzione Python standard hello nella  **[Python.org Scarica](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="69dda-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="69dda-107">Molti sviluppatori trovano hello pratico toouse  **[distribuzione Anaconda Python](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="69dda-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="69dda-108">Questo articolo è stato scritto usando Python versione 3.6 dalla distribuzione di Python standard hello</span><span class="sxs-lookup"><span data-stu-id="69dda-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="69dda-109">Installare Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="69dda-109">Install Azure Python SDK</span></span>

<span data-ttu-id="69dda-110">Installare hello seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="69dda-110">Install hello following modules:</span></span>

* <span data-ttu-id="69dda-111">Hello **-mgmt-risorse di azure** modulo include altri moduli di Azure per Active Directory e così via.</span><span class="sxs-lookup"><span data-stu-id="69dda-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="69dda-112">Hello **archivio azure-mgmt-Lake** modulo include operazioni di gestione di account archivio Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="69dda-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="69dda-113">Hello **dell'archivio Lake azure** modulo include le operazioni di file System di hello archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69dda-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="69dda-114">Hello **azure-Lake-analitica** modulo include le operazioni di Azure Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="69dda-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="69dda-115">In primo luogo, verificare di aver hello più recente `pip` eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="69dda-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="69dda-116">Questo documento si basa su `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="69dda-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="69dda-117">Utilizzare la seguente hello `pip` comandi moduli hello tooinstall dalla riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="69dda-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="69dda-118">Creare un nuovo script Python</span><span class="sxs-lookup"><span data-stu-id="69dda-118">Create a new Python script</span></span>

<span data-ttu-id="69dda-119">Incollare hello seguente di codice in script hello:</span><span class="sxs-lookup"><span data-stu-id="69dda-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="69dda-120">Eseguire questo tooverify script che hello moduli possono essere importati.</span><span class="sxs-lookup"><span data-stu-id="69dda-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="69dda-121">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="69dda-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="69dda-122">Autenticazione utente interattiva con un popup</span><span class="sxs-lookup"><span data-stu-id="69dda-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="69dda-123">Questo metodo non è supportato.</span><span class="sxs-lookup"><span data-stu-id="69dda-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="69dda-124">Autenticazione utente interattiva con un codice di dispositivo</span><span class="sxs-lookup"><span data-stu-id="69dda-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="69dda-125">Autenticazione non interattiva con una SPI e un segreto</span><span class="sxs-lookup"><span data-stu-id="69dda-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="69dda-126">Autenticazione non interattiva con un'API e un certificato</span><span class="sxs-lookup"><span data-stu-id="69dda-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="69dda-127">Questo metodo non è supportato.</span><span class="sxs-lookup"><span data-stu-id="69dda-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="69dda-128">Variabili dello script comuni</span><span class="sxs-lookup"><span data-stu-id="69dda-128">Common script variables</span></span>

<span data-ttu-id="69dda-129">Queste variabili vengono utilizzate negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="69dda-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="69dda-130">Creare i client hello</span><span class="sxs-lookup"><span data-stu-id="69dda-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="69dda-131">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="69dda-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="69dda-132">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="69dda-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="69dda-133">Creare prima un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="69dda-133">First create a store account.</span></span>

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
<span data-ttu-id="69dda-134">Creare quindi un account ADLA che usa tale archivio.</span><span class="sxs-lookup"><span data-stu-id="69dda-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="69dda-135">Inviare un processo</span><span class="sxs-lookup"><span data-stu-id="69dda-135">Submit a job</span></span>

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
    too"/data.csv"
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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="69dda-136">Attendere un tooend processo</span><span class="sxs-lookup"><span data-stu-id="69dda-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="69dda-137">Elencare pipeline e ricorrenze</span><span class="sxs-lookup"><span data-stu-id="69dda-137">List pipelines and recurrences</span></span>
<span data-ttu-id="69dda-138">A seconda se i processi hanno pipeline o metadati associati, è possibile elencare le pipeline e le ricorrenze.</span><span class="sxs-lookup"><span data-stu-id="69dda-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="69dda-139">Gestire i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="69dda-139">Manage compute policies</span></span>

<span data-ttu-id="69dda-140">oggetto DataLakeAnalyticsAccountManagementClient Hello fornisce metodi per la gestione di hello calcolano criteri per un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="69dda-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="69dda-141">Elencare i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="69dda-141">List compute policies</span></span>

<span data-ttu-id="69dda-142">Hello seguente codice recupera un elenco di criteri di calcolo per un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="69dda-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="69dda-143">Creare un nuovo criterio di calcolo</span><span class="sxs-lookup"><span data-stu-id="69dda-143">Create a new compute policy</span></span>

<span data-ttu-id="69dda-144">Hello di codice seguente crea un nuovo criterio di calcolo per un account Data Lake Analitica, impostazione hello massimo AUs disponibile toohello specificato utente too50 e hello processo minimo priorità too250.</span><span class="sxs-lookup"><span data-stu-id="69dda-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="69dda-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69dda-145">Next steps</span></span>

- <span data-ttu-id="69dda-146">toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="69dda-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="69dda-147">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="69dda-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="69dda-148">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69dda-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

