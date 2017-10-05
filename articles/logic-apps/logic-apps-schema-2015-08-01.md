---
title: "Aggiornamenti dello schema del 1° agosto 2015 in anteprima: App per la logica di Azure | Microsoft Docs"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="b164b-103">Aggiornamenti dello schema per App per la logica di Azure: anteprima del 1° agosto 2015</span><span class="sxs-lookup"><span data-stu-id="b164b-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="b164b-104">La nuova versione dello schema e dell'API per App per la logica di Azure include importanti miglioramenti che rendono le app per la logica più affidabili e facili da usare:</span><span class="sxs-lookup"><span data-stu-id="b164b-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="b164b-105">Il tipo di azione **APIApp** viene aggiornato e sostituito con un nuovo tipo di azione [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="b164b-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="b164b-106">**Repeat** viene rinominato come [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="b164b-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="b164b-107">L'[app per le API **Listener HTTP**](#http-listener) non è più necessaria.</span><span class="sxs-lookup"><span data-stu-id="b164b-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="b164b-108">La chiamata a flussi di lavoro figlio usa un [nuovo schema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="b164b-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="b164b-109">Passare alle connessioni API</span><span class="sxs-lookup"><span data-stu-id="b164b-109">Move to API connections</span></span>

<span data-ttu-id="b164b-110">Il cambiamento più importante riguarda il fatto che non è più necessario distribuire app per le API nella sottoscrizione di Azure per poter usare le API.</span><span class="sxs-lookup"><span data-stu-id="b164b-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="b164b-111">Ecco in che modo è possibile usare le API:</span><span class="sxs-lookup"><span data-stu-id="b164b-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="b164b-112">API gestite</span><span class="sxs-lookup"><span data-stu-id="b164b-112">Managed APIs</span></span>
* <span data-ttu-id="b164b-113">API Web personalizzate</span><span class="sxs-lookup"><span data-stu-id="b164b-113">Your custom Web APIs</span></span>

<span data-ttu-id="b164b-114">Ciascun metodo viene gestito in modo leggermente diverso perché prevede modelli di gestione e hosting diversi.</span><span class="sxs-lookup"><span data-stu-id="b164b-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="b164b-115">Un vantaggio di questo modello è che non si è più vincolati a risorse che vengono distribuite nel gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b164b-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="b164b-116">API gestite</span><span class="sxs-lookup"><span data-stu-id="b164b-116">Managed APIs</span></span>

<span data-ttu-id="b164b-117">Microsoft gestisce alcune API per conto dell'utente, ad esempio Office 365, Salesforce, Twitter e FTP.</span><span class="sxs-lookup"><span data-stu-id="b164b-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="b164b-118">È possibile usare alcune API gestite così come sono, ad esempio Bing Translate, mentre altre richiedono una configurazione.</span><span class="sxs-lookup"><span data-stu-id="b164b-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="b164b-119">Questa configurazione è detta *connessione*.</span><span class="sxs-lookup"><span data-stu-id="b164b-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="b164b-120">Quando si usa Office 365, ad esempio, è necessario creare una connessione contenente il token di accesso a Office 365.</span><span class="sxs-lookup"><span data-stu-id="b164b-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="b164b-121">Il token è archiviato in modo sicuro e aggiornato in modo che l'app per la logica possa sempre chiamare l'API di Office 365.</span><span class="sxs-lookup"><span data-stu-id="b164b-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="b164b-122">In alternativa, per connettersi al server SQL o FTP è necessario creare una connessione che includa la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="b164b-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="b164b-123">In questa definizione, queste azioni sono denominate `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="b164b-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="b164b-124">Di seguito è riportato un esempio di connessione che chiama Office 365 per inviare un messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="b164b-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="b164b-125">L'oggetto `host` è la porzione di input univoca per le connessioni API e contiene due parti: `api` e `connection`.</span><span class="sxs-lookup"><span data-stu-id="b164b-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="b164b-126">`api` contiene l'URL di runtime della posizione in cui è ospitata l'API gestita.</span><span class="sxs-lookup"><span data-stu-id="b164b-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="b164b-127">Per visualizzare tutte le API gestite disponibili, è possibile chiamare `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="b164b-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="b164b-128">Quando si usa un'API, questa può presentare o meno *parametri di connessione* definiti.</span><span class="sxs-lookup"><span data-stu-id="b164b-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="b164b-129">Se non sono definiti, non è richiesta alcuna *connessione*.</span><span class="sxs-lookup"><span data-stu-id="b164b-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="b164b-130">Se sono definiti, è necessario creare una connessione.</span><span class="sxs-lookup"><span data-stu-id="b164b-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="b164b-131">La connessione creata ha il nome scelto.</span><span class="sxs-lookup"><span data-stu-id="b164b-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="b164b-132">Poi si fa riferimento al nome nell'oggetto `connection` all'interno dell'oggetto `host`.</span><span class="sxs-lookup"><span data-stu-id="b164b-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="b164b-133">Per creare una connessione in un gruppo di risorse, chiamare:</span><span class="sxs-lookup"><span data-stu-id="b164b-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="b164b-134">Con il corpo seguente:</span><span class="sxs-lookup"><span data-stu-id="b164b-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="b164b-135">Distribuire API gestite in un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b164b-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="b164b-136">È possibile creare un'applicazione completa in un modello di Azure Resource Manager, purché non sia necessario l'accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="b164b-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="b164b-137">Se è necessario l'accesso, è possibile impostare tutto con il modello di Azure Resource Manager, ma sarà comunque necessario visitare il portale per autorizzare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="b164b-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="b164b-138">Come si vede in questo esempio, le connessioni non sono altro che risorse presenti nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b164b-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="b164b-139">Fanno riferimento alle API gestite disponibili nella sottoscrizione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b164b-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="b164b-140">API Web personalizzate</span><span class="sxs-lookup"><span data-stu-id="b164b-140">Your custom Web APIs</span></span>

<span data-ttu-id="b164b-141">Se si usano API personalizzate, non quelle gestite da Microsoft, usare l'azione **HTTP** predefinita per chiamarle.</span><span class="sxs-lookup"><span data-stu-id="b164b-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="b164b-142">Per un'esperienza ideale, si consiglia di esporre un endpoint swagger per l'API.</span><span class="sxs-lookup"><span data-stu-id="b164b-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="b164b-143">Questo endpoint consente alla finestra di progettazione di app per la logica di eseguire il rendering degli input e degli output per l'API.</span><span class="sxs-lookup"><span data-stu-id="b164b-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="b164b-144">Senza Swagger, la finestra di progettazione può mostrare gli input e gli output solo come oggetti JSON opachi.</span><span class="sxs-lookup"><span data-stu-id="b164b-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="b164b-145">Di seguito è riportato un esempio che mostra la nuova proprietà `metadata.apiDefinitionUrl` :</span><span class="sxs-lookup"><span data-stu-id="b164b-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="b164b-146">Se l'API Web è ospitata in Servizio app di Azure, verrà visualizzata automaticamente nell'elenco di azioni disponibili nella finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b164b-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="b164b-147">In caso contrario, è necessario incollare direttamente l'URL.</span><span class="sxs-lookup"><span data-stu-id="b164b-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="b164b-148">Per poter essere usato nella finestra di progettazione di app per la logica, l'endpoint Swagger deve essere non autenticato, anche se è possibile proteggere l'API stessa con qualsiasi metodo supportato da Swagger.</span><span class="sxs-lookup"><span data-stu-id="b164b-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="b164b-149">Chiamare le app per le API già distribuite con 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="b164b-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="b164b-150">Se in precedenza è stata distribuita un'app per le API, è possibile chiamare l'app usando l'azione **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="b164b-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="b164b-151">Ad esempio, se si usa Dropbox per elencare i file, la definizione della versione dello schema **2014-12-01-preview** può essere simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b164b-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="b164b-152">È possibile costruire l'azione HTTP equivalente come nell'esempio seguente, mentre la sezione parameters della definizione dell'app per la logica rimane invariata:</span><span class="sxs-lookup"><span data-stu-id="b164b-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="b164b-153">La tabella seguente illustra le singole proprietà:</span><span class="sxs-lookup"><span data-stu-id="b164b-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="b164b-154">Proprietà dell'azione</span><span class="sxs-lookup"><span data-stu-id="b164b-154">Action property</span></span> | <span data-ttu-id="b164b-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b164b-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="b164b-156">`Http` anziché `APIapp`</span><span class="sxs-lookup"><span data-stu-id="b164b-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="b164b-157">Per usare questa azione nella finestra di progettazione di app per la logica, includere l'endpoint dei metadati, costituito da: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="b164b-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="b164b-158">Costituito da: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="b164b-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="b164b-159">Sempre `POST`</span><span class="sxs-lookup"><span data-stu-id="b164b-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="b164b-160">Identica ai parametri dell'app per le API</span><span class="sxs-lookup"><span data-stu-id="b164b-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="b164b-161">Identica all'autenticazione dell'app per le API</span><span class="sxs-lookup"><span data-stu-id="b164b-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="b164b-162">Questo approccio dovrebbe funzionare per tutte le azioni delle app per le API.</span><span class="sxs-lookup"><span data-stu-id="b164b-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="b164b-163">Tenere tuttavia presente che queste app per le api precedenti non sono più supportate.</span><span class="sxs-lookup"><span data-stu-id="b164b-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="b164b-164">È quindi consigliabile passare a una delle altre due opzioni precedenti, un'API gestita o l'hosting dell'API Web personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b164b-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="b164b-165">"Repeat" rinominato come "foreach"</span><span class="sxs-lookup"><span data-stu-id="b164b-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="b164b-166">In base ai commenti e suggerimenti ricevuti dai clienti per la versione dello schema precedente, **Ripeti** generava confusione e non era chiaramente identificabile come ciclo **Foreach** .</span><span class="sxs-lookup"><span data-stu-id="b164b-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="b164b-167">Di conseguenza, `repeat` è stato rinominato in `foreach`.</span><span class="sxs-lookup"><span data-stu-id="b164b-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="b164b-168">Ad esempio, in precedenza si sarebbe scritto:</span><span class="sxs-lookup"><span data-stu-id="b164b-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="b164b-169">Ora si scriverebbe:</span><span class="sxs-lookup"><span data-stu-id="b164b-169">Now you would write:</span></span>

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

<span data-ttu-id="b164b-170">In precedenza veniva usata la funzione `@repeatItem()` per fare riferimento all'elemento corrente sottoposto a iterazione.</span><span class="sxs-lookup"><span data-stu-id="b164b-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="b164b-171">Questa funzione è ora semplificata a `@item()`.</span><span class="sxs-lookup"><span data-stu-id="b164b-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="b164b-172">Fare riferimento agli output da "foreach"</span><span class="sxs-lookup"><span data-stu-id="b164b-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="b164b-173">Per maggiore semplicità, non viene eseguito il wrapping degli output dalle azioni `foreach` in un oggetto denominato `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="b164b-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="b164b-174">Mentre gli output dall'esempio di `repeat` precedente erano:</span><span class="sxs-lookup"><span data-stu-id="b164b-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="b164b-175">Ora tali output sono:</span><span class="sxs-lookup"><span data-stu-id="b164b-175">Now these outputs are:</span></span>

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

<span data-ttu-id="b164b-176">Prima per ottenere il corpo dell'azione facendo riferimento agli output, era necessario eseguire:</span><span class="sxs-lookup"><span data-stu-id="b164b-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="b164b-177">Ora, invece, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="b164b-177">Now you can do instead:</span></span>

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

<span data-ttu-id="b164b-178">Con queste modifiche, le funzioni `@repeatItem()`, `@repeatBody()` e `@repeatOutputs()` sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="b164b-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="b164b-179">Listener HTTP nativo</span><span class="sxs-lookup"><span data-stu-id="b164b-179">Native HTTP listener</span></span>

<span data-ttu-id="b164b-180">Le funzionalità del listener HTTP ora sono predefinite.</span><span class="sxs-lookup"><span data-stu-id="b164b-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="b164b-181">Non è quindi più necessario distribuire un'app per le API del listener HTTP.</span><span class="sxs-lookup"><span data-stu-id="b164b-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="b164b-182">Per informazioni dettagliate, vedere [App per la logica come endpoint che è possibile chiamare](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b164b-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="b164b-183">Con queste modifiche, è stata rimossa la funzione `@accessKeys()`, che è stata sostituita con la funzione `@listCallbackURL()` per ottenere l'endpoint, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b164b-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="b164b-184">Ora è anche necessario definire almeno un trigger nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b164b-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="b164b-185">Per eseguire il comando `/run` sul flusso di lavoro, è necessario avere un trigger `manual`, `apiConnectionWebhook` o `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="b164b-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="b164b-186">Chiamare flussi di lavoro figlio</span><span class="sxs-lookup"><span data-stu-id="b164b-186">Call child workflows</span></span>

<span data-ttu-id="b164b-187">In precedenza, per la chiamata a flussi di lavoro figlio era necessario passare al flusso di lavoro, ottenere il token di accesso e incollare il token nella definizione dell'app per la logica in cui si vuole chiamare tale flusso di lavoro figlio.</span><span class="sxs-lookup"><span data-stu-id="b164b-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="b164b-188">Con il nuovo schema, il motore di app per la logica genera automaticamente una firma di accesso condiviso in fase di esecuzione per il flusso di lavoro figlio, quindi non è necessario incollare segreti nella definizione.</span><span class="sxs-lookup"><span data-stu-id="b164b-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="b164b-189">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="b164b-189">Here is an example:</span></span>

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

<span data-ttu-id="b164b-190">Un secondo miglioramento è l'accesso completo alla richiesta in ingresso per i flussi di lavoro figlio.</span><span class="sxs-lookup"><span data-stu-id="b164b-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="b164b-191">Ciò significa che è possibile passare parametri nella sezione *queries* e nell'oggetto *headers* e che è possibile definire completamente l'intero corpo.</span><span class="sxs-lookup"><span data-stu-id="b164b-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="b164b-192">Infine, è stato necessario apportare modifiche al flusso di lavoro figlio.</span><span class="sxs-lookup"><span data-stu-id="b164b-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="b164b-193">Mentre in precedenza era possibile chiamare direttamente un flusso di lavoro figlio, ora occorre definire un endpoint trigger nel flusso di lavoro che l'elemento padre possa chiamare.</span><span class="sxs-lookup"><span data-stu-id="b164b-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="b164b-194">In genere, si aggiungerà un trigger con il tipo `manual` da usare nella definizione dell'elemento padre.</span><span class="sxs-lookup"><span data-stu-id="b164b-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="b164b-195">Si noti che la proprietà `host` in particolare include un `triggerName`, perché è sempre necessario specificare quale trigger viene richiamato.</span><span class="sxs-lookup"><span data-stu-id="b164b-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="b164b-196">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="b164b-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="b164b-197">Nuova proprietà "queries"</span><span class="sxs-lookup"><span data-stu-id="b164b-197">New 'queries' property</span></span>

<span data-ttu-id="b164b-198">Tutti i tipi di azione ora supportano un nuovo input denominato `queries`.</span><span class="sxs-lookup"><span data-stu-id="b164b-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="b164b-199">Questo input può essere un oggetto strutturato e non è più necessario assemblare la stringa manualmente.</span><span class="sxs-lookup"><span data-stu-id="b164b-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="b164b-200">Funzione "parse()" rinominata come "json()"</span><span class="sxs-lookup"><span data-stu-id="b164b-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="b164b-201">Verranno aggiunti a breve altri tipi di contenuti, quindi la funzione `parse()` è stata rinominata `json()`.</span><span class="sxs-lookup"><span data-stu-id="b164b-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="b164b-202">Presto disponibile: API Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="b164b-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="b164b-203">Non sono ancora disponibili versioni gestite delle API Enterprise Integration, ad esempio AS2.</span><span class="sxs-lookup"><span data-stu-id="b164b-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="b164b-204">Per il momento è possibile usare le API di BizTalk distribuite tramite l'azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="b164b-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="b164b-205">Per informazioni dettagliate, vedere "Using your already deployed API apps" (Uso delle app per le API già distribuite) nella [guida di orientamento all'integrazione](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="b164b-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
