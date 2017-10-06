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
# <a name="manage-azure-data-lake-analytics-using-python"></a>Gestire Azure Data Lake Analytics con Python

## <a name="python-versions"></a>Versioni di Python

* Usare una versione a 64 bit di Python.
* È possibile utilizzare distribuzione Python standard hello nella  **[Python.org Scarica](https://www.python.org/downloads/)**. 
* Molti sviluppatori trovano hello pratico toouse  **[distribuzione Anaconda Python](https://www.continuum.io/downloads)**.  
* Questo articolo è stato scritto usando Python versione 3.6 dalla distribuzione di Python standard hello

## <a name="install-azure-python-sdk"></a>Installare Azure Python SDK

Installare hello seguenti moduli:

* Hello **-mgmt-risorse di azure** modulo include altri moduli di Azure per Active Directory e così via.
* Hello **archivio azure-mgmt-Lake** modulo include operazioni di gestione di account archivio Azure Data Lake hello.
* Hello **dell'archivio Lake azure** modulo include le operazioni di file System di hello archivio Azure Data Lake. 
* Hello **azure-Lake-analitica** modulo include le operazioni di Azure Data Lake Analitica hello. 

In primo luogo, verificare di aver hello più recente `pip` eseguendo hello comando seguente:

```
python -m pip install --upgrade pip
```

Questo documento si basa su `pip version 9.0.1`.

Utilizzare la seguente hello `pip` comandi moduli hello tooinstall dalla riga di comando hello:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Creare un nuovo script Python

Incollare hello seguente di codice in script hello:

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

Eseguire questo tooverify script che hello moduli possono essere importati.

## <a name="authentication"></a>Autenticazione

### <a name="interactive-user-authentication-with-a-pop-up"></a>Autenticazione utente interattiva con un popup

Questo metodo non è supportato.

### <a name="interactive-user-authentication-with-a-device-code"></a>Autenticazione utente interattiva con un codice di dispositivo

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Autenticazione non interattiva con una SPI e un segreto

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Autenticazione non interattiva con un'API e un certificato

Questo metodo non è supportato.

## <a name="common-script-variables"></a>Variabili dello script comuni

Queste variabili vengono utilizzate negli esempi di hello.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Creare i client hello

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Creare un gruppo di risorse di Azure

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Creare un account di Analisi Data Lake

Creare prima un account di archiviazione.

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
Creare quindi un account ADLA che usa tale archivio.

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

## <a name="submit-a-job"></a>Inviare un processo

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

## <a name="wait-for-a-job-tooend"></a>Attendere un tooend processo

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Elencare pipeline e ricorrenze
A seconda se i processi hanno pipeline o metadati associati, è possibile elencare le pipeline e le ricorrenze.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Gestire i criteri di calcolo

oggetto DataLakeAnalyticsAccountManagementClient Hello fornisce metodi per la gestione di hello calcolano criteri per un account Data Lake Analitica.

### <a name="list-compute-policies"></a>Elencare i criteri di calcolo

Hello seguente codice recupera un elenco di criteri di calcolo per un account Data Lake Analitica.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Creare un nuovo criterio di calcolo

Hello di codice seguente crea un nuovo criterio di calcolo per un account Data Lake Analitica, impostazione hello massimo AUs disponibile toohello specificato utente too50 e hello processo minimo priorità too250.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Passaggi successivi

- toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.
- toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).
- Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).

