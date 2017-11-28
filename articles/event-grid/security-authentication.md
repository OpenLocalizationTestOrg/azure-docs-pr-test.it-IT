---
title: autenticazione e sicurezza griglia eventi aaaAzure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="06f19-103">Sicurezza e autenticazione di Griglia di eventi</span><span class="sxs-lookup"><span data-stu-id="06f19-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="06f19-104">Griglia di eventi di Azure ha tre tipi di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="06f19-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="06f19-105">Sottoscrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="06f19-105">Event subscriptions</span></span>
* <span data-ttu-id="06f19-106">Pubblicazione di eventi</span><span class="sxs-lookup"><span data-stu-id="06f19-106">Event publishing</span></span>
* <span data-ttu-id="06f19-107">Recapito eventi webhook</span><span class="sxs-lookup"><span data-stu-id="06f19-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="06f19-108">Recapito eventi webhook</span><span class="sxs-lookup"><span data-stu-id="06f19-108">WebHook Event delivery</span></span>

<span data-ttu-id="06f19-109">Webhook sono uno dei molti eventi di tooreceive modi in tempo reale dalla griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="06f19-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="06f19-110">Ogni volta che è presente un nuovo toobe pronto evento recapitato, griglia eventi invia una richiesta HTTP con tooyour WebHook con evento hello nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="06f19-111">Quando si registra il proprio endpoint WebHook con griglia di eventi, invia una richiesta POST con un codice di convalida semplice della proprietà di endpoint tooprove ordine.</span><span class="sxs-lookup"><span data-stu-id="06f19-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="06f19-112">L'app deve toorespond visualizzando il codice di convalida hello indietro.</span><span class="sxs-lookup"><span data-stu-id="06f19-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="06f19-113">Griglia di eventi non fornirà eventi tooWebHook endpoint che non hanno superato la convalida di hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="06f19-114">Informazioni di convalida:</span><span class="sxs-lookup"><span data-stu-id="06f19-114">Validation details:</span></span>

* <span data-ttu-id="06f19-115">In fase di hello di creazione/aggiornamento della sottoscrizione evento, evento griglia registra un endpoint di destinazione "SubscriptionValidationEvent" toohello evento.</span><span class="sxs-lookup"><span data-stu-id="06f19-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="06f19-116">evento Hello contiene un valore di intestazione "Convalida di tipo di evento:".</span><span class="sxs-lookup"><span data-stu-id="06f19-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="06f19-117">corpo dell'evento Hello è hello stesso schema di altri eventi di griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="06f19-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="06f19-118">dati dell'evento Hello includono una proprietà di "ValidationCode" con una stringa generata in modo casuale, ad esempio "ValidationCode: acb13…".</span><span class="sxs-lookup"><span data-stu-id="06f19-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="06f19-119">In proprietà di endpoint tooprove ordine, echo ad esempio di codice convalida hello Indietro "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="06f19-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="06f19-120">Infine, è importante toonote che griglia di eventi di Azure supporta solo l'endpoint webhook HTTPS.</span><span class="sxs-lookup"><span data-stu-id="06f19-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="06f19-121">Sottoscrizione dell'evento</span><span class="sxs-lookup"><span data-stu-id="06f19-121">Event subscription</span></span>

<span data-ttu-id="06f19-122">evento tooan toosubscribe, è necessario disporre hello **Microsoft.EventGrid/EventSubscriptions/Write** risorsa necessaria l'autorizzazione in hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="06f19-123">Questa autorizzazione è necessaria poiché si sta creando una nuova sottoscrizione nell'ambito di hello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="06f19-124">Hello necessarie risorse varia in base al se si effettua la sottoscrizione dell'argomento di sistema di tooa o argomento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="06f19-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="06f19-125">Entrambi i tipi sono descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="06f19-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="06f19-126">Argomenti di sistema (entità di pubblicazione dei servizi di Azure)</span><span class="sxs-lookup"><span data-stu-id="06f19-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="06f19-127">Gli argomenti di sistema, è necessario autorizzazione toowrite una nuova sottoscrizione di eventi nell'ambito di hello dell'evento di hello hello risorse pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="06f19-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="06f19-128">formato Hello della risorsa hello è:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="06f19-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="06f19-129">Ad esempio, toosubscribe tooan evento su un account di archiviazione denominato **myacct**, è richiesta l'autorizzazione di Microsoft.EventGrid/EventSubscriptions/Write hello in:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="06f19-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="06f19-130">Argomenti personalizzati</span><span class="sxs-lookup"><span data-stu-id="06f19-130">Custom topics</span></span>

<span data-ttu-id="06f19-131">Per argomenti personalizzati, è necessario autorizzazione toowrite una nuova sottoscrizione di eventi nell'ambito di hello di argomento evento griglia hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="06f19-132">formato Hello della risorsa hello è:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="06f19-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="06f19-133">Ad esempio, toosubscribe tooa argomento personalizzato denominato **mytopic**, è richiesta l'autorizzazione di Microsoft.EventGrid/EventSubscriptions/Write hello in:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="06f19-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="06f19-134">Pubblicazione di argomenti</span><span class="sxs-lookup"><span data-stu-id="06f19-134">Topic publishing</span></span>

<span data-ttu-id="06f19-135">Gli argomenti usano la firma di accesso condiviso o l'autenticazione della chiave.</span><span class="sxs-lookup"><span data-stu-id="06f19-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="06f19-136">È consigliabile la firma di accesso condiviso, ma l'autenticazione della chiave fornisce una programmazione semplice ed è compatibile con molte entità di pubblicazione di webhook esistenti.</span><span class="sxs-lookup"><span data-stu-id="06f19-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="06f19-137">Includere il valore di autenticazione hello nell'intestazione HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="06f19-138">Per la firma di accesso condiviso, utilizzare **token di firma di accesso condiviso aeg** per il valore dell'intestazione hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="06f19-139">Per l'autenticazione con chiave, utilizzare **chiave di firma di accesso condiviso aeg** per il valore dell'intestazione hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="06f19-140">Autenticazione della chiave</span><span class="sxs-lookup"><span data-stu-id="06f19-140">Key authentication</span></span>

<span data-ttu-id="06f19-141">L'autenticazione con chiave è più semplice di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="06f19-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="06f19-142">Utilizzare il formato: hello`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="06f19-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="06f19-143">Ad esempio, passare una chiave con:</span><span class="sxs-lookup"><span data-stu-id="06f19-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="06f19-144">Token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="06f19-144">SAS tokens</span></span>

<span data-ttu-id="06f19-145">I token di firma di accesso condiviso per griglia di eventi includono risorse hello, un'ora di scadenza e una firma.</span><span class="sxs-lookup"><span data-stu-id="06f19-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="06f19-146">Hello formato del token di firma di accesso condiviso hello è: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="06f19-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="06f19-147">risorsa Hello è il percorso di hello per hello argomento toowhich si invia eventi.</span><span class="sxs-lookup"><span data-stu-id="06f19-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="06f19-148">Un percorso di risorsa valido, ad esempio, è: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="06f19-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="06f19-149">Firma hello generate da una chiave.</span><span class="sxs-lookup"><span data-stu-id="06f19-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="06f19-150">Un valore **aeg-sas-token** valido, ad esempio, è:</span><span class="sxs-lookup"><span data-stu-id="06f19-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="06f19-151">Hello di esempio seguente crea un token di firma di accesso condiviso per l'utilizzo con griglia eventi:</span><span class="sxs-lookup"><span data-stu-id="06f19-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="06f19-152">Controllo di accesso per la gestione</span><span class="sxs-lookup"><span data-stu-id="06f19-152">Management Access Control</span></span>

<span data-ttu-id="06f19-153">Azure griglia di eventi consente si toocontrol hello livello di accesso assegnato toodifferent utenti toodo varie operazioni di gestione, ad esempio le sottoscrizioni di eventi di elenco, crearne di nuovi e generare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="06f19-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="06f19-154">Griglia di eventi utilizza a questo scopo il controllo degli accessi in base al ruolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="06f19-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="06f19-155">Tipi di operazioni</span><span class="sxs-lookup"><span data-stu-id="06f19-155">Operation types</span></span>

<span data-ttu-id="06f19-156">Griglia di eventi di Azure supporta hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="06f19-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="06f19-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="06f19-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="06f19-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="06f19-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="06f19-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="06f19-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="06f19-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="06f19-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="06f19-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="06f19-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="06f19-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="06f19-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="06f19-163">Hello ultime tre operazioni restituito potenzialmente informazioni segrete Ottiene filtrato da normale operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="06f19-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="06f19-164">È consigliabile per consentire operazioni di toothese toorestrict accesso.</span><span class="sxs-lookup"><span data-stu-id="06f19-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="06f19-165">È possibile creare ruoli personalizzati utilizzando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure interfaccia della riga di comando (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), hello e [API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="06f19-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="06f19-166">Applicazione del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="06f19-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="06f19-167">Utilizzare hello seguendo i passaggi tooenforce RBAC per utenti diversi:</span><span class="sxs-lookup"><span data-stu-id="06f19-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="06f19-168">Creare un file di definizione del ruolo personalizzato (JSON)</span><span class="sxs-lookup"><span data-stu-id="06f19-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="06f19-169">di seguito Hello sono definizioni di ruolo della griglia di eventi di esempio che consentono agli utenti tooperform diversi set di azioni.</span><span class="sxs-lookup"><span data-stu-id="06f19-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="06f19-170">**EventGridReadOnlyRole.json**: consente solo operazioni di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="06f19-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="06f19-171">**EventGridNoDeleteListKeysRole.json**: consente le azioni di pubblicazione con restrizioni, ma non consente le azioni di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="06f19-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="06f19-172">**EventGridContributorRole.json**: consente tutte le azioni di Griglia di eventi.</span><span class="sxs-lookup"><span data-stu-id="06f19-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="06f19-173">Installazione e account di accesso tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="06f19-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="06f19-174">Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="06f19-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="06f19-175">versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="06f19-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="06f19-176">Azure Resource Manager nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="06f19-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="06f19-177">Andare troppo[Using hello CLI di Azure con Gestione risorse di hello](../xplat-cli-azure-resource-manager.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="06f19-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="06f19-178">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="06f19-178">Create a custom role</span></span>

<span data-ttu-id="06f19-179">toocreate un ruolo personalizzato, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="06f19-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="06f19-180">Assegnare hello ruolo tooa utente</span><span class="sxs-lookup"><span data-stu-id="06f19-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="06f19-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06f19-181">Next steps</span></span>

* <span data-ttu-id="06f19-182">Per un'introduzione tooEvent griglia, vedere [sulla griglia di eventi](overview.md)</span><span class="sxs-lookup"><span data-stu-id="06f19-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
