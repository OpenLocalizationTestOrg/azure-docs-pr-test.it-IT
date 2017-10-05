---
title: Sicurezza e autenticazione di Griglia di eventi di Azure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="17c59-103">Sicurezza e autenticazione di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="17c59-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="17c59-104">Griglia di eventi di Azure ha tre tipi di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="17c59-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="17c59-105">Sottoscrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="17c59-105">Event subscriptions</span></span>
* <span data-ttu-id="17c59-106">Pubblicazione di eventi</span><span class="sxs-lookup"><span data-stu-id="17c59-106">Event publishing</span></span>
* <span data-ttu-id="17c59-107">Recapito eventi webhook</span><span class="sxs-lookup"><span data-stu-id="17c59-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="17c59-108">Recapito eventi webhook</span><span class="sxs-lookup"><span data-stu-id="17c59-108">WebHook Event delivery</span></span>

<span data-ttu-id="17c59-109">I webhook sono uno dei modi per ricevere gli eventi in tempo reale da Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="17c59-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="17c59-110">Ogni volta che un nuovo evento è pronto per essere recapitato, Griglia di eventi invia al webhook una richiesta HTTP nel cui corpo è contenuto l'evento.</span><span class="sxs-lookup"><span data-stu-id="17c59-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="17c59-111">Quando si registra l'endpoint del webhook con Griglia di eventi, viene inviata una richiesta POST con un semplice codice di convalida per dimostrare la proprietà dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="17c59-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="17c59-112">È necessario che l'app risponda rimandando il codice di convalida.</span><span class="sxs-lookup"><span data-stu-id="17c59-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="17c59-113">Griglia di eventi non recapiterà gli eventi agli endpoint del webhook che non hanno superato la convalida.</span><span class="sxs-lookup"><span data-stu-id="17c59-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="17c59-114">Informazioni di convalida:</span><span class="sxs-lookup"><span data-stu-id="17c59-114">Validation details:</span></span>

* <span data-ttu-id="17c59-115">In fase di creazione/aggiornamento della sottoscrizione dell'evento, Griglia di eventi pubblica un evento "SubscriptionValidationEvent" nell'endpoint di destinazione.</span><span class="sxs-lookup"><span data-stu-id="17c59-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="17c59-116">L'evento contiene un valore di intestazione "Event-Type: Validation".</span><span class="sxs-lookup"><span data-stu-id="17c59-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="17c59-117">Il corpo dell'evento ha lo stesso schema degli altri eventi di Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="17c59-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="17c59-118">I dati dell'evento includono una proprietà "ValidationCode" con una stringa generata in modo casuale, ad esempio "ValidationCode: acb13…".</span><span class="sxs-lookup"><span data-stu-id="17c59-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="17c59-119">Per dimostrare la proprietà dell'endpoint, rimandare il codice di convalida, ad esempio "ValidationResponse: acb13…".</span><span class="sxs-lookup"><span data-stu-id="17c59-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="17c59-120">È infine importante notare che Griglia di eventi di Azure supporta solo endpoint di webhook HTTPS.</span><span class="sxs-lookup"><span data-stu-id="17c59-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="17c59-121">Sottoscrizione dell'evento</span><span class="sxs-lookup"><span data-stu-id="17c59-121">Event subscription</span></span>

<span data-ttu-id="17c59-122">Per sottoscrivere un evento, è necessaria l'autorizzazione **Microsoft.EventGrid/EventSubscriptions/Write** per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="17c59-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="17c59-123">Questa autorizzazione è necessaria perché si sta scrivendo una nuova sottoscrizione nell'ambito della risorsa.</span><span class="sxs-lookup"><span data-stu-id="17c59-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="17c59-124">La risorsa necessaria è diversa a seconda del fatto che si sottoscriva un argomento di sistema o un argomento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="17c59-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="17c59-125">Entrambi i tipi sono descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="17c59-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="17c59-126">Argomenti di sistema (entità di pubblicazione dei servizi di Azure)</span><span class="sxs-lookup"><span data-stu-id="17c59-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="17c59-127">Per gli argomenti di sistema, è necessaria l'autorizzazione per scrivere una nuova sottoscrizione di evento nell'ambito della risorsa che pubblica l'evento.</span><span class="sxs-lookup"><span data-stu-id="17c59-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="17c59-128">Il formato della risorsa è: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="17c59-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="17c59-129">Per sottoscrivere, ad esempio, un evento in un account di archiviazione denominato **myacct**, è necessaria l'autorizzazione Microsoft.EventGrid/EventSubscriptions/Write per: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="17c59-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="17c59-130">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="17c59-130">Custom topics</span></span>

<span data-ttu-id="17c59-131">Per gli argomenti personalizzati, è necessaria l'autorizzazione per scrivere una nuova sottoscrizione di evento nell'ambito dell'argomento di Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="17c59-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="17c59-132">Il formato della risorsa è: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="17c59-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="17c59-133">Per sottoscrivere, ad esempio, un argomento personalizzato denominato **mytopic**, è necessaria l'autorizzazione Microsoft.EventGrid/EventSubscriptions/Write per: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="17c59-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="17c59-134">Pubblicazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="17c59-134">Topic publishing</span></span>

<span data-ttu-id="17c59-135">Gli argomenti usano la firma di accesso condiviso o l'autenticazione della chiave.</span><span class="sxs-lookup"><span data-stu-id="17c59-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="17c59-136">È consigliabile la firma di accesso condiviso, ma l'autenticazione della chiave fornisce una programmazione semplice ed è compatibile con molte entità di pubblicazione di webhook esistenti.</span><span class="sxs-lookup"><span data-stu-id="17c59-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="17c59-137">Il valore dell'autenticazione viene incluso nell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="17c59-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="17c59-138">Per la firma di accesso condiviso, usare **aeg-sas-token** per il valore dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="17c59-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="17c59-139">Per l'autenticazione della chiave, usare **aeg-sas-key** per il valore dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="17c59-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="17c59-140">Autenticazione della chiave</span><span class="sxs-lookup"><span data-stu-id="17c59-140">Key authentication</span></span>

<span data-ttu-id="17c59-141">L'autenticazione della chiave è la forma più semplice di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="17c59-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="17c59-142">Usare il formato: `aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="17c59-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="17c59-143">Ad esempio, passare una chiave con:</span><span class="sxs-lookup"><span data-stu-id="17c59-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="17c59-144">Token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="17c59-144">SAS tokens</span></span>

<span data-ttu-id="17c59-145">I token di firma di accesso condiviso per Griglia di eventi includono la risorsa, un'ora di scadenza e una firma.</span><span class="sxs-lookup"><span data-stu-id="17c59-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="17c59-146">Il formato del token di firma di accesso condiviso è: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="17c59-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="17c59-147">La risorsa è il percorso dell'argomento a cui si inviano gli eventi.</span><span class="sxs-lookup"><span data-stu-id="17c59-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="17c59-148">Un percorso di risorsa valido, ad esempio, è: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="17c59-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="17c59-149">La firma viene generata da una chiave.</span><span class="sxs-lookup"><span data-stu-id="17c59-149">You generate the signature from a key.</span></span>

<span data-ttu-id="17c59-150">Un valore **aeg-sas-token** valido, ad esempio, è:</span><span class="sxs-lookup"><span data-stu-id="17c59-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="17c59-151">L'esempio seguente crea un token di firma di accesso condiviso per l'uso con Griglia di eventi:</span><span class="sxs-lookup"><span data-stu-id="17c59-151">The following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="17c59-152">Controllo di accesso per la gestione</span><span class="sxs-lookup"><span data-stu-id="17c59-152">Management Access Control</span></span>

<span data-ttu-id="17c59-153">Griglia di eventi di Azure consente di controllare il livello di accesso assegnato ai diversi utenti per eseguire svariate operazioni di gestione, ad esempio elencare sottoscrizioni di eventi, crearne di nuove e generare chiavi.</span><span class="sxs-lookup"><span data-stu-id="17c59-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="17c59-154">Griglia di eventi utilizza a questo scopo il controllo degli accessi in base al ruolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="17c59-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="17c59-155">Tipi di operazioni</span><span class="sxs-lookup"><span data-stu-id="17c59-155">Operation types</span></span>

<span data-ttu-id="17c59-156">Griglia di eventi di Azure supporta le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="17c59-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="17c59-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="17c59-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="17c59-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="17c59-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="17c59-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="17c59-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="17c59-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="17c59-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="17c59-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="17c59-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="17c59-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="17c59-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="17c59-163">Le ultime tre operazioni restituiscono informazioni potenzialmente riservate che vengono filtrate dalle normali operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="17c59-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="17c59-164">È consigliabile limitare l'accesso a queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="17c59-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="17c59-165">I ruoli personalizzati possono essere creati usando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [l'interfaccia della riga di comando di Azure (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md) e la [API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="17c59-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="17c59-166">Applicazione del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="17c59-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="17c59-167">Usare i passaggi seguenti per applicare il controllo degli accessi in base al ruolo per utenti diversi:</span><span class="sxs-lookup"><span data-stu-id="17c59-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="17c59-168">Creare un file di definizione del ruolo personalizzato (JSON)</span><span class="sxs-lookup"><span data-stu-id="17c59-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="17c59-169">Le seguenti sono definizioni del ruolo di Griglia di eventi che consentono agli utenti di eseguire set diversi di azioni.</span><span class="sxs-lookup"><span data-stu-id="17c59-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="17c59-170">**EventGridReadOnlyRole.json**: consente solo operazioni di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="17c59-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="17c59-171">**EventGridNoDeleteListKeysRole.json**: consente le azioni di pubblicazione con restrizioni, ma non consente le azioni di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="17c59-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="17c59-172">**EventGridContributorRole.json**: consente tutte le azioni di Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="17c59-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="17c59-173">Installare e accedere all'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="17c59-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="17c59-174">Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="17c59-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="17c59-175">Per installare la versione più recente e associarla alla sottoscrizione di Azure, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="17c59-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="17c59-176">Azure Resource Manager nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="17c59-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="17c59-177">Per altre informazioni, vedere [Uso dell'interfaccia della riga di comando di Azure con Resource Manager](../xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="17c59-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="17c59-178">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="17c59-178">Create a custom role</span></span>

<span data-ttu-id="17c59-179">Per creare un ruolo personalizzato, usare:</span><span class="sxs-lookup"><span data-stu-id="17c59-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="17c59-180">Assegnare il ruolo a un utente</span><span class="sxs-lookup"><span data-stu-id="17c59-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="17c59-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17c59-181">Next steps</span></span>

* <span data-ttu-id="17c59-182">Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md).</span><span class="sxs-lookup"><span data-stu-id="17c59-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
