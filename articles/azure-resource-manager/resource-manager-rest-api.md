---
title: API REST di gestione aaaResource | Documenti Microsoft
description: Cenni preliminari hello autenticazione API REST di gestione risorse ed esempi di utilizzo
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>API REST di Resource Manager
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfaccia della riga di comando di Azure](xplat-cli-azure-resource-manager.md)
> * [Portale](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Dietro tooAzure ogni chiamata di gestione risorse, associate a ogni modello distribuito, dietro ogni account di archiviazione configurato non esistono API REST di uno o più chiamate toohello Azure del gestore delle risorse. In questo argomento è dedicato toothose API e come è possibile chiamare senza usare affatto qualsiasi SDK. Questo approccio è utile se si desidera il controllo completo di richieste tooAzure o se hello SDK per la lingua preferita non è disponibile o non supporta le operazioni di hello che è necessario.

In questo articolo non passa attraverso tutte le API viene esposta in Azure, ma alcune operazioni utilizzano come esempi delle modalità di connessione toothem. Dopo aver compreso i concetti di base hello, è possibile leggere hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind informazioni dettagliate su come toouse hello restanti hello API.

## <a name="authentication"></a>Autenticazione
L'autenticazione per Resource Manager viene gestita da Azure Active Directory (AD). tooconnect tooany API, è necessario innanzitutto tooauthenticate con Azure AD tooreceive un token di autenticazione che è possibile passare a tooevery richiesta. Come ci stiamo che descrive una chiamata pura direttamente toohello API REST, si presuppone che non si desidera tooauthenticate da viene richiesto un nome utente e password. Si suppone inoltre che l'utente non usi i meccanismi di autenticazione a due fattori. Pertanto, si costituiscono un'applicazione Azure AD e un'entità servizio che vengono utilizzati toolog in. Ma si tenga presente che Azure AD supporta diverse procedure di autenticazione e tutti gli elementi può essere utilizzato tooretrieve tale token di autenticazione necessarie per le successive richieste API.
Per istruzioni dettagliate, vedere [Creare un'applicazione e un'entità servizio di Azure AD](resource-group-create-service-principal-portal.md).

### <a name="generating-an-access-token"></a>Generazione di un token di accesso
L'autenticazione con Azure AD viene eseguita da una chiamata in uscita tooAzure AD, disponibile all'indirizzo login.microsoftonline.com. tooauthenticate, è necessario hello toohave le seguenti informazioni:

* ID del Tenant Azure Active Directory (nome ad Azure AD si utilizza toolog in hello, spesso hello come la società ma non necessaria)
* ID dell'applicazione (prese durante il passaggio della creazione dell'applicazione hello Azure AD)
* Password (che è stata selezionata durante la creazione di hello applicazione Azure AD)

In hello seguente richiesta HTTP, assicurarsi che tooreplace "ID Tenant di Azure AD," "ID applicazione" e "Password" con i valori corretti di hello.

**Richiesta HTTP generica:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... verrà (se l'autenticazione ha esito positivo) produce una toohello simile di risposta seguente risposta:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(access_token hello in hello risposta precedente sono stati tooincrease abbreviato leggibilità)

**Generazione del token di accesso con Bash:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Generazione del token di accesso con Powershell:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

risposta Hello contiene un token di accesso, informazioni sulla durata token è valido e informazioni su quali risorse è possibile usare tale token per.
token di accesso Hello ricevuti nella chiamata HTTP precedente hello devono essere passati per toohello richiesta tutte le API di gestione risorse. Viene passato come un valore di intestazione denominato "Authorization" con valore hello "Portatore YOUR_ACCESS_TOKEN". Si noti lo spazio di hello tra "Bearer" e il token di accesso.

Come si può vedere dal hello sopra i risultati di HTTP, hello token è valido per un determinato periodo di tempo durante i quali è necessario memorizzare nella cache e riutilizzare i token stesso. Anche se è possibile tooauthenticate con Azure AD per ogni chiamata API, sarebbe particolarmente inefficiente.

## <a name="calling-resource-manager-rest-apis"></a>Chiamata alle API REST di Gestione risorse
In questo argomento Usa solo alcune API tooexplain hello l'utilizzo di base di operazioni REST hello. Per informazioni su tutte le operazioni di hello, vedere [le API REST di gestione risorse di Azure](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Elenco di tutte le sottoscrizioni
Una delle operazioni di hello più semplice che è possibile eseguire è toolist hello sottoscrizioni disponibili che è possibile accedere. Hello seguito richiesta, è visualizzato come token di accesso hello viene passato come un'intestazione di:

Sostituire YOUR_ACCESS_TOKEN con il token di accesso vero e proprio.

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... e di conseguenza, si visualizza un elenco di sottoscrizioni che tooaccess è consentita da questa entità servizio

(Gli ID sottoscrizione seguenti sono stati abbreviati per renderli più leggibili)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Elencare tutti i gruppi di risorse in una sottoscrizione specifica
Tutte le risorse disponibili con le API di gestione risorse di hello sono annidate all'interno di un gruppo di risorse. È possibile eseguire query di gestione risorse di gruppi di risorse esistente nella sottoscrizione tramite hello seguente richiesta HTTP GET. Si noti come ID di sottoscrizione hello viene passato come parte dell'URL hello questo momento.

(Sostituire YOUR_ACCESS_TOKEN e SUBSCRIPTION_ID con il token di accesso e l'ID sottoscrizione effettivi)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Hello risposta ottenuta varia a seconda se si dispone di gruppi di risorse definiti e in tal caso, il numero.

(Gli ID sottoscrizione seguenti sono stati abbreviati per renderli più leggibili)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Finora è stato solo stato query hello le API di gestione risorse per informazioni. È ora è creare alcune risorse e per iniziare, hello più semplice di visualizzarli tutti, un gruppo di risorse. Hello richiesta HTTP seguente crea un gruppo di risorse in una regione di propria scelta e aggiunge tooit un tag.

(Sostituire YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME con l'effettivo Token di accesso, ID sottoscrizione e nome del gruppo di risorse da toocreate hello)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

Se ha esito positivo, si otterrà una risposta simile toohello seguente risposta:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

È stato creato un gruppo di risorse in Azure. Congratulazioni.

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Distribuire un gruppo di risorse tooa di risorse mediante un modello di gestione risorse
Con Gestione risorse, è possibile distribuire le risorse usando i modelli. Un modello definisce diverse risorse e le relative dipendenze. In questa sezione si presuppone che si ha familiarità con i modelli di gestione risorse e solo illustrare come API hello toomake chiama toostart distribuzione. Per altre informazioni sulla creazione dei modelli, vedere [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creazione di modelli di Gestione risorse).

Distribuzione di un modello non differiscono molto toohow è chiamare altre API. Un aspetto importante è che la distribuzione di un modello può richiedere molto tempo. Restituisce solo una chiamata API Hello ed è attivo tooyou come tooquery developer per lo stato di hello distribuzione toofind out quando hello distribuzione viene eseguita. Per ulteriori informazioni, vedere [Track asynchronous Azure operations](resource-manager-async-operations.md) (Tenere traccia delle operazioni asincrone di Azure).

Per questo esempio, verrà usato un modello esposto pubblicamente disponibile su [GitHub](https://github.com/Azure/azure-quickstart-templates). modello Hello che utilizziamo consente di distribuire un'area di Stati Uniti occidentali toohello VM Linux. Anche se viene utilizzato un modello disponibile in un archivio pubblico come GitHub, è invece possibile passare modello completo hello come parte della richiesta di hello. Si noti che vengono forniti i valori di parametro nella richiesta di hello utilizzati all'interno di hello distribuzione modello.

(Sostituire SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD e DNS_NAME_FOR_PUBLIC_IP toovalues appropriato per la richiesta)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

risposta JSON lunghi Hello per questa richiesta è stato omesso tooimprove leggibilità di questa documentazione. risposta Hello contiene informazioni sulla distribuzione basata su modelli hello creato.

## <a name="next-steps"></a>Passaggi successivi

- toolearn sulla gestione di operazioni asincrone di REST, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).
