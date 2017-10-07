---
title: aaaSchema Aggiorna anteprima di agosto-1-2015 - App Azure per la logica | Documenti Microsoft
description: Creare definizioni JSON per App per la logica di Azure con la versione dello schema 2015-08-01-preview
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="bfa29-103">Aggiornamenti dello schema per App per la logica di Azure: anteprima del 1° agosto 2015</span><span class="sxs-lookup"><span data-stu-id="bfa29-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="bfa29-104">Questo nuovo schema e l'API di versione per App di logica di Azure include importanti miglioramenti che App per la logica di rendere più affidabile e facile toouse:</span><span class="sxs-lookup"><span data-stu-id="bfa29-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="bfa29-105">Hello **APIApp** tipo di azione è aggiornato tooa nuova [ **APIConnection** ](#api-connections) tipo di azione.</span><span class="sxs-lookup"><span data-stu-id="bfa29-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="bfa29-106">**Ripetere** viene rinominato troppo[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="bfa29-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="bfa29-107">Hello [ **HTTP Listener** App per le API](#http-listener) non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="bfa29-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="bfa29-108">La chiamata a flussi di lavoro figlio usa un [nuovo schema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="bfa29-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="bfa29-109">Spostare le connessioni tooAPI</span><span class="sxs-lookup"><span data-stu-id="bfa29-109">Move tooAPI connections</span></span>

<span data-ttu-id="bfa29-110">cambiamento Hello è che non è più necessario toodeploy App per le API alla sottoscrizione di Azure è possibile utilizzare le API.</span><span class="sxs-lookup"><span data-stu-id="bfa29-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="bfa29-111">Esistono metodi hello che è possibile utilizzare le API:</span><span class="sxs-lookup"><span data-stu-id="bfa29-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="bfa29-112">API gestite</span><span class="sxs-lookup"><span data-stu-id="bfa29-112">Managed APIs</span></span>
* <span data-ttu-id="bfa29-113">API Web personalizzate</span><span class="sxs-lookup"><span data-stu-id="bfa29-113">Your custom Web APIs</span></span>

<span data-ttu-id="bfa29-114">Ciascun metodo viene gestito in modo leggermente diverso perché prevede modelli di gestione e hosting diversi.</span><span class="sxs-lookup"><span data-stu-id="bfa29-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="bfa29-115">Uno dei vantaggi di questo modello è non sta non è più vincolata tooresources che vengono distribuite nel gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa29-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="bfa29-116">API gestite</span><span class="sxs-lookup"><span data-stu-id="bfa29-116">Managed APIs</span></span>

<span data-ttu-id="bfa29-117">Microsoft gestisce alcune API per conto dell'utente, ad esempio Office 365, Salesforce, Twitter e FTP.</span><span class="sxs-lookup"><span data-stu-id="bfa29-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="bfa29-118">È possibile usare alcune API gestite così come sono, ad esempio Bing Translate, mentre altre richiedono una configurazione.</span><span class="sxs-lookup"><span data-stu-id="bfa29-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="bfa29-119">Questa configurazione è detta *connessione*.</span><span class="sxs-lookup"><span data-stu-id="bfa29-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="bfa29-120">Quando si usa Office 365, ad esempio, è necessario creare una connessione contenente il token di accesso a Office 365.</span><span class="sxs-lookup"><span data-stu-id="bfa29-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="bfa29-121">Questo token in modo sicuro è archiviato e aggiornato in modo che l'app logica può chiamare sempre il metodo hello API di Office 365.</span><span class="sxs-lookup"><span data-stu-id="bfa29-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="bfa29-122">In alternativa, se si desidera tooconnect tooyour FTP o SQL server, è necessario creare una connessione con la stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="bfa29-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="bfa29-123">In questa definizione, queste azioni sono denominate `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="bfa29-124">Di seguito è riportato un esempio di una connessione che chiama un messaggio di posta elettronica di Office 365 toosend:</span><span class="sxs-lookup"><span data-stu-id="bfa29-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-125">Hello `host` oggetto è parte di input connessioni tooAPI univoco, che contiene due parti: `api` e `connection`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="bfa29-126">Hello `api` ha runtime hello URL dell'API che gestita con una diversa in cui è ospitato.</span><span class="sxs-lookup"><span data-stu-id="bfa29-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="bfa29-127">È possibile visualizzare tutti hello disponibili API gestite chiamando `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="bfa29-128">Quando si utilizza un'API, hello API potrebbe o potrebbe non disporre *parametri di connessione* definito.</span><span class="sxs-lookup"><span data-stu-id="bfa29-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="bfa29-129">Se non hello API, nessun *connessione* è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="bfa29-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="bfa29-130">In caso di hello API, è necessario creare una connessione.</span><span class="sxs-lookup"><span data-stu-id="bfa29-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="bfa29-131">nome di hello prescelto connessione Hello creato.</span><span class="sxs-lookup"><span data-stu-id="bfa29-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="bfa29-132">Per fare riferimento nome hello in hello `connection` oggetto all'interno di hello `host` oggetto.</span><span class="sxs-lookup"><span data-stu-id="bfa29-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="bfa29-133">una connessione in un gruppo di risorse, chiamata toocreate:</span><span class="sxs-lookup"><span data-stu-id="bfa29-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="bfa29-134">Con hello corpo seguente:</span><span class="sxs-lookup"><span data-stu-id="bfa29-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="bfa29-135">Distribuire API gestite in un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfa29-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="bfa29-136">È possibile creare un'applicazione completa in un modello di Azure Resource Manager, purché non sia necessario l'accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="bfa29-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="bfa29-137">Se l'accesso è obbligatorio, è possibile impostare tutti gli elementi con il modello di gestione risorse di Azure hello, ma è comunque necessario connessioni di hello toovisit hello tooauthorize portale.</span><span class="sxs-lookup"><span data-stu-id="bfa29-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="bfa29-138">È possibile visualizzare in questo esempio le connessioni hello sono solo le risorse che risiedono nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bfa29-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="bfa29-139">Fanno riferimento a tooyou disponibili di API gestita hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bfa29-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="bfa29-140">API Web personalizzate</span><span class="sxs-lookup"><span data-stu-id="bfa29-140">Your custom Web APIs</span></span>

<span data-ttu-id="bfa29-141">Se si utilizzano le tue API, quelli non gestiti da Microsoft, utilizzare incorporato hello **HTTP** toocall azione li.</span><span class="sxs-lookup"><span data-stu-id="bfa29-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="bfa29-142">Per un'esperienza ideale, si consiglia di esporre un endpoint swagger per l'API.</span><span class="sxs-lookup"><span data-stu-id="bfa29-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="bfa29-143">Questo endpoint consente gli input di hello progettazione applicazione logica toorender hello e output per l'API.</span><span class="sxs-lookup"><span data-stu-id="bfa29-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="bfa29-144">Senza Swagger, progettazione hello può mostrare solo hello input e output come oggetti JSON opachi.</span><span class="sxs-lookup"><span data-stu-id="bfa29-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="bfa29-145">Ecco un hello di esempio che mostra nuova `metadata.apiDefinitionUrl` proprietà:</span><span class="sxs-lookup"><span data-stu-id="bfa29-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-146">Se si ospita l'API Web nel servizio App di Azure, l'API Web viene visualizzato automaticamente nell'elenco di hello di azioni disponibili nella finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="bfa29-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="bfa29-147">In caso contrario, sono presenti toopaste URL hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="bfa29-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="bfa29-148">endpoint Swagger Hello deve essere non autenticate toobe utilizzabile in hello progettazione applicazione logica, anche se è possibile proteggere hello stessa interfaccia API con qualsiasi metodo che supporta Swagger.</span><span class="sxs-lookup"><span data-stu-id="bfa29-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="bfa29-149">Chiamare le app per le API già distribuite con 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="bfa29-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="bfa29-150">Se già stato distribuito un'App per le API, è possibile chiamare l'applicazione hello con hello **HTTP** azione.</span><span class="sxs-lookup"><span data-stu-id="bfa29-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="bfa29-151">Ad esempio, se si utilizzano file toolist dell'area di sincronizzazione, il **2014-12-01-preview** definizione di versione dello schema potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bfa29-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="bfa29-152">È possibile costruire azione HTTP equivalente hello simile a questo esempio, mentre sezione parametri hello di definizione dell'app logica hello rimane invariato:</span><span class="sxs-lookup"><span data-stu-id="bfa29-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="bfa29-153">La tabella seguente illustra le singole proprietà:</span><span class="sxs-lookup"><span data-stu-id="bfa29-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="bfa29-154">Proprietà dell'azione</span><span class="sxs-lookup"><span data-stu-id="bfa29-154">Action property</span></span> | <span data-ttu-id="bfa29-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bfa29-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="bfa29-156">`Http` anziché `APIapp`</span><span class="sxs-lookup"><span data-stu-id="bfa29-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="bfa29-157">toouse in hello progettazione applicazione logica, questa azione includono l'endpoint dei metadati hello, che viene creato da:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="bfa29-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="bfa29-158">Costituito da: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="bfa29-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="bfa29-159">Sempre `POST`</span><span class="sxs-lookup"><span data-stu-id="bfa29-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="bfa29-160">Parametri dell'App toohello identici API</span><span class="sxs-lookup"><span data-stu-id="bfa29-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="bfa29-161">L'autenticazione di App per le API di toohello identico</span><span class="sxs-lookup"><span data-stu-id="bfa29-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="bfa29-162">Questo approccio dovrebbe funzionare per tutte le azioni delle app per le API.</span><span class="sxs-lookup"><span data-stu-id="bfa29-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="bfa29-163">Tenere tuttavia presente che queste app per le api precedenti non sono più supportate.</span><span class="sxs-lookup"><span data-stu-id="bfa29-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="bfa29-164">È pertanto consigliabile spostare tooone di hello due altre opzioni precedenti, un'API gestita o ospita l'API Web personalizzato.</span><span class="sxs-lookup"><span data-stu-id="bfa29-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="bfa29-165">Rinominare 'repeat' too'foreach'</span><span class="sxs-lookup"><span data-stu-id="bfa29-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="bfa29-166">Per la versione di schema hello precedente, è pervenuta quantità i suggerimenti dei clienti che **ripetere** creava notevole confusione e che non è stata correttamente acquisire **ripetere** fosse effettivamente un ciclo foreach.</span><span class="sxs-lookup"><span data-stu-id="bfa29-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="bfa29-167">Di conseguenza, è stata rinominata `repeat` troppo`foreach`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="bfa29-168">Ad esempio, in precedenza si sarebbe scritto:</span><span class="sxs-lookup"><span data-stu-id="bfa29-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-169">Ora si scriverebbe:</span><span class="sxs-lookup"><span data-stu-id="bfa29-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-170">funzione Hello `@repeatItem()` è stato utilizzato in precedenza tooreference elemento corrente di hello scorsa.</span><span class="sxs-lookup"><span data-stu-id="bfa29-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="bfa29-171">Questa funzione è ora semplificata troppo`@item()`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="bfa29-172">Fare riferimento agli output da "foreach"</span><span class="sxs-lookup"><span data-stu-id="bfa29-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="bfa29-173">Per semplificare le operazioni, gli output hello `foreach` azioni non sono incapsulate in un oggetto denominato `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="bfa29-174">Mentre hello di output di hello precedente `repeat` esempio fosse:</span><span class="sxs-lookup"><span data-stu-id="bfa29-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="bfa29-175">Ora tali output sono:</span><span class="sxs-lookup"><span data-stu-id="bfa29-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="bfa29-176">In precedenza, il tooget toohello corpo dell'azione di hello quando si fa riferimento a questi output:</span><span class="sxs-lookup"><span data-stu-id="bfa29-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-177">Ora, invece, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="bfa29-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="bfa29-178">Con queste modifiche, hello funzioni `@repeatItem()`, `@repeatBody()`, e `@repeatOutputs()` vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="bfa29-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="bfa29-179">Listener HTTP nativo</span><span class="sxs-lookup"><span data-stu-id="bfa29-179">Native HTTP listener</span></span>

<span data-ttu-id="bfa29-180">Hello funzionalità HTTP Listener sono ora incorporate.</span><span class="sxs-lookup"><span data-stu-id="bfa29-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="bfa29-181">Pertanto, non è più necessario toodeploy un'App per le API del Listener HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfa29-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="bfa29-182">Vedere [hello dettagli completi per informazioni su come toomake il qui callable di logica app endpoint](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="bfa29-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="bfa29-183">Con queste modifiche, sono state rimosse hello `@accessKeys()` funzione, pertanto abbiamo sostituito con hello `@listCallbackURL()` funzione per ottenere l'endpoint di hello quando necessario.</span><span class="sxs-lookup"><span data-stu-id="bfa29-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="bfa29-184">Ora è anche necessario definire almeno un trigger nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="bfa29-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="bfa29-185">Se si desidera troppo`/run` hello del flusso di lavoro, è necessario disporre di uno di questi trigger: `manual`, `apiConnectionWebhook`, o `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="bfa29-186">Chiamare flussi di lavoro figlio</span><span class="sxs-lookup"><span data-stu-id="bfa29-186">Call child workflows</span></span>

<span data-ttu-id="bfa29-187">In precedenza, la chiamata di flussi di lavoro figlio, è necessario passare toohello del flusso di lavoro, ottenere il token di accesso di hello e concatenamento dei token di hello nella definizione di applicazione hello logica in cui si desidera toocall tale flusso di lavoro figlio.</span><span class="sxs-lookup"><span data-stu-id="bfa29-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="bfa29-188">Con nuovo schema hello, hello logica App motore genera automaticamente una firma di accesso condiviso in fase di esecuzione per hello del flusso di lavoro figlio in modo da non avere troppo incollato alcun dato segreto definizione hello.</span><span class="sxs-lookup"><span data-stu-id="bfa29-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="bfa29-189">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="bfa29-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="bfa29-190">Un secondo miglioramento è che verrà ugualmente figlio hello richiesta in ingresso toohello accesso completo di flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bfa29-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="bfa29-191">Ciò significa che è possibile passare parametri hello *query* sezione e in hello *intestazioni* oggetto e che è possibile definire completamente hello intero corpo.</span><span class="sxs-lookup"><span data-stu-id="bfa29-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="bfa29-192">Infine, sono presenti flussi di lavoro figlio toohello le modifiche necessarie.</span><span class="sxs-lookup"><span data-stu-id="bfa29-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="bfa29-193">Mentre in precedenza è possibile chiamare direttamente un flusso di lavoro figlio, a questo punto è necessario definire un endpoint di trigger nel flusso di lavoro di hello per toocall padre hello.</span><span class="sxs-lookup"><span data-stu-id="bfa29-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="bfa29-194">In genere, si aggiunge un trigger con `manual` digitare e quindi utilizzare tale trigger nella definizione di hello padre.</span><span class="sxs-lookup"><span data-stu-id="bfa29-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="bfa29-195">Hello nota `host` proprietà di un `triggerName` perché è sempre necessario specificare i trigger di cui si sta chiamando.</span><span class="sxs-lookup"><span data-stu-id="bfa29-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="bfa29-196">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="bfa29-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="bfa29-197">Nuova proprietà "queries"</span><span class="sxs-lookup"><span data-stu-id="bfa29-197">New 'queries' property</span></span>

<span data-ttu-id="bfa29-198">Tutti i tipi di azione ora supportano un nuovo input denominato `queries`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="bfa29-199">L'input può essere un oggetto strutturato, anziché dover stringa hello tooassemble manualmente.</span><span class="sxs-lookup"><span data-stu-id="bfa29-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="bfa29-200">Rinominato too'json() funzione 'Parse ()' '</span><span class="sxs-lookup"><span data-stu-id="bfa29-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="bfa29-201">Si sta aggiungendo a breve, i tipi di contenuto più in modo hello è stato rinominato `parse()` funzione troppo`json()`.</span><span class="sxs-lookup"><span data-stu-id="bfa29-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="bfa29-202">Presto disponibile: API Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="bfa29-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="bfa29-203">Non è gestite versioni ancora hello Enterprise Integration API, ad esempio AS2.</span><span class="sxs-lookup"><span data-stu-id="bfa29-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="bfa29-204">Nel frattempo, è possibile utilizzare le APIs BizTalk distribuito esistente tramite hello azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfa29-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="bfa29-205">Per informazioni dettagliate, vedere "Utilizzo delle App già distribuite API" in hello [roadmap integrazione](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="bfa29-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
