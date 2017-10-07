---
title: dati da Azure Log Analitica tooretrieve degli script aaaPython | Documenti Microsoft
description: API di ricerca Log Analitica Log Hello consente qualsiasi client dell'API REST tooretrieve dati da un'area di lavoro Log Analitica.  Questo articolo fornisce uno script Python di esempio tramite l'API di ricerca Log hello.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: bwren
ms.openlocfilehash: a45693b04cd388301b859e7186ca671786d0229e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a>Recuperare i dati da Log Analytics con uno script Python
Hello [API di ricerca Log Analitica Log](log-analytics-log-search-api.md) consente a qualsiasi client dell'API REST tooretrieve dati da un'area di lavoro Log Analitica.  In questo articolo presenta uno script Python di esempio che utilizza l'API di ricerca Log Analitica Log hello.  

## <a name="authentication"></a>Autenticazione
Questo script utilizza un'entità servizio dell'area di lavoro di Azure Active Directory tooauthenticate toohello.  Le entità servizio consentono a un client applicazione toorequest che hello servizio autenticare un account anche se hello client non dispone di nome dell'account hello. Prima di eseguire questo script, è necessario creare un'entità servizio tramite il processo di hello in [utilizzare portale toocreate un'applicazione Azure Active Directory e dell'entità servizio che possono accedere alle risorse](../azure-resource-manager/resource-group-create-service-principal-portal.md).  È necessario tooprovide hello ID applicazione, ID Tenant e chiave di autenticazione toohello script. 

> [!NOTE]
> Quando si [creare un account di automazione di Azure](../automation/automation-create-standalone-account.md), un'entità servizio viene creata toouse adatto con questo script.  Se si dispone già di un'entità servizio creata di automazione di Azure, dovrebbe essere in grado di toouse, anziché crearne uno nuovo, anche se potrebbe essere troppo[creare una chiave di autenticazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) se non ne ha già uno.

## <a name="script"></a>Script
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these tooyour requirements.
query = "Type=Event"
end_time = datetime.datetime.utcnow()
start_time = end_time - datetime.timedelta(hours=24)
num_results = 100  # If not provided, a default of 10 results will be used.

# IDs for authentication.  Fill in values for your service principal.
subscription_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
tenant_id = 'xxxxxxxx-xxxx-xxxx-xxx-xxxxxxxxxxxx'
application_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx'
application_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

# URLs for authentication
authentication_endpoint = 'https://login.microsoftonline.com/'
resource  = 'https://management.core.windows.net/'

# Get access token
context = adal.AuthenticationContext('https://login.microsoftonline.com/' + tenant_id)
token_response = context.acquire_token_with_client_credentials('https://management.core.windows.net/', application_id, application_key)
access_token = token_response.get('accessToken')

# Add token tooheader
headers = {
    "Authorization": 'Bearer ' + access_token,
    "Content-Type":'application/json'
}

# URLs for retrieving data
uri_base = 'https://management.azure.com'
uri_api = 'api-version=2015-11-01-preview'
uri_subscription = 'https://management.azure.com/subscriptions/' + subscription_id
uri_resourcegroup = uri_subscription + '/resourcegroups/'+ resource_group
uri_workspace = uri_resourcegroup + '/providers/Microsoft.OperationalInsights/workspaces/' + workspace
uri_search = uri_workspace + '/search'

# Build search parameters from query details
search_params = {
        "query": query,
        "top": num_results,
        "start": start_time.strftime('%Y-%m-%dT%H:%M:%S'),
        "end": end_time.strftime('%Y-%m-%dT%H:%M:%S')
        }

# Build URL and send post request
uri = uri_search + '?' + uri_api
response = requests.post(uri,json=search_params,headers=headers)

# Response of 200 if successful
if response.status_code == 200:

    # Parse hello response tooget hello ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL tooget search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse hello response tooget hello status
        data = response.json()
        status = data["__metadata"]["Status"]

else:

    # Request failed
    print (response.status_code)
    response.raise_for_status()

print ("Total records:" + str(data["__metadata"]["total"]))
print ("Returned top:" + str(data["__metadata"]["top"]))
pprint (data["value"])
```
## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su hello [API di ricerca Log Analitica Log](log-analytics-log-search-api.md).
