---
title: Proteggere l'accesso alle app per la logica di Azure | Documentazione Microsoft
description: Aggiungere la sicurezza per la protezione dell'accesso ai trigger, agli input e output, ai parametri di azione e ai servizi utilizzati con i flussi di lavoro nelle app per la logica di Azure.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="d5fec-103">Proteggere l'accesso alle app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-103">Secure access to your logic apps</span></span>

<span data-ttu-id="d5fec-104">Sono disponibili molti strumenti per proteggere un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d5fec-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="d5fec-105">Protezione dell'accesso per attivare un'app per la logica (trigger di una richiesta HTTP)</span><span class="sxs-lookup"><span data-stu-id="d5fec-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="d5fec-106">Protezione dell'accesso per gestire, modificare o leggere un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="d5fec-107">Protezione dell'accesso ai contenuti di input e output per un'esecuzione</span><span class="sxs-lookup"><span data-stu-id="d5fec-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="d5fec-108">Protezione di parametri o input all'interno di azioni in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="d5fec-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="d5fec-109">Protezione dell'accesso ai servizi che ricevono richieste da un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="d5fec-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="d5fec-110">Proteggere l'accesso al trigger</span><span class="sxs-lookup"><span data-stu-id="d5fec-110">Secure access to trigger</span></span>

<span data-ttu-id="d5fec-111">Quando si lavora con un'app per la logica che viene attivata con una richiesta HTTP ([richiesta](../connectors/connectors-native-reqres.md) o [webhook](../connectors/connectors-native-webhook.md)), è possibile limitare l'accesso in modo che possa essere attivata solo dai client autorizzati.</span><span class="sxs-lookup"><span data-stu-id="d5fec-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="d5fec-112">Tutte le richieste in un'app per la logica vengono crittografate e protette tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="d5fec-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="d5fec-113">Firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="d5fec-113">Shared Access Signature</span></span>

<span data-ttu-id="d5fec-114">Ogni endpoint di richiesta per un'app per la logica include una [firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) come parte dell'URL.</span><span class="sxs-lookup"><span data-stu-id="d5fec-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="d5fec-115">Ogni URL contiene parametri di query `sp`, `sv` e `sig`.</span><span class="sxs-lookup"><span data-stu-id="d5fec-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="d5fec-116">Le autorizzazioni vengono specificate da `sp` e corrispondono ai metodi HTTP consentiti, `sv` è la versione usata per generare e `sig` è il parametro usato per autenticare l'accesso al trigger.</span><span class="sxs-lookup"><span data-stu-id="d5fec-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="d5fec-117">La firma viene generata attraverso l'algoritmo SHA256 con una chiave privata in tutti i percorsi e le proprietà dell'URL.</span><span class="sxs-lookup"><span data-stu-id="d5fec-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="d5fec-118">La chiave privata non viene mai esposta né pubblicata, inoltre continua a essere crittografata e archiviata nell'ambito dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d5fec-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="d5fec-119">L'app per la logica autorizza solo i trigger che contengono una firma valida creata con la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d5fec-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="d5fec-120">Per rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="d5fec-120">Regenerate access keys</span></span>

<span data-ttu-id="d5fec-121">È possibile rigenerare in qualsiasi momento una nuova chiave protetta tramite il portale di Azure o API REST.</span><span class="sxs-lookup"><span data-stu-id="d5fec-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="d5fec-122">Tutti gli URL correnti che sono stati generati in passato usando la chiave precedente verranno invalidati e non saranno più autorizzati ad attivare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d5fec-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="d5fec-123">Nel Portale di Azure aprire l'app per la logica per cui si desidera rigenerare una chiave.</span><span class="sxs-lookup"><span data-stu-id="d5fec-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="d5fec-124">Fare clic sulla voce di menu **Chiavi di accesso** in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5fec-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="d5fec-125">Scegliere la chiave da rigenerare e completare il processo.</span><span class="sxs-lookup"><span data-stu-id="d5fec-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="d5fec-126">Per accedere agli URL recuperati dopo la rigenerazione, è necessaria la nuova chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="d5fec-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="d5fec-127">Creazione di URL di callback con una data di scadenza</span><span class="sxs-lookup"><span data-stu-id="d5fec-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="d5fec-128">Se si condivide l'URL con altre parti, è possibile generare gli URL con chiavi e date di scadenza specifiche in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d5fec-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="d5fec-129">Questo consente di eseguire perfettamente il roll delle chiavi o di verificare che l'accesso per attivare un'app sia limitato a un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d5fec-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="d5fec-130">È possibile specificare una data di scadenza per un URL tramite l'[API REST delle app per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="d5fec-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="d5fec-131">Nel corpo includere la proprietà `NotAfter` come una stringa di data JSON, che restituisce un URL di callback valido solo fino a data e ora `NotAfter`.</span><span class="sxs-lookup"><span data-stu-id="d5fec-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="d5fec-132">Creazione di URL con una chiave privata primaria o secondaria</span><span class="sxs-lookup"><span data-stu-id="d5fec-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="d5fec-133">Quando si generano URL di callback per i trigger basati su richieste o si crea un elenco che li contiene, è anche possibile specificare la chiave da usare per firmare l'URL.</span><span class="sxs-lookup"><span data-stu-id="d5fec-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="d5fec-134">È possibile generare un URL firmato da una chiave specifica tramite l'[API REST delle app per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d5fec-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="d5fec-135">Nel corpo includere la proprietà `KeyType` come `Primary` o `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="d5fec-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="d5fec-136">Viene restituito un URL firmato dalla chiave sicura specificata.</span><span class="sxs-lookup"><span data-stu-id="d5fec-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="d5fec-137">Limitare gli indirizzi IP in ingresso</span><span class="sxs-lookup"><span data-stu-id="d5fec-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="d5fec-138">Oltre alla firma di accesso condiviso, si potrebbe voler limitare la chiamata a un'app per la logica solo da client specifici.</span><span class="sxs-lookup"><span data-stu-id="d5fec-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="d5fec-139">Ad esempio, se si gestisce l'endpoint tramite Gestione API di Azure, è possibile limitare l'app per la logica in modo che accetti solo le richieste provenienti dall'indirizzo IP dell'istanza di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="d5fec-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="d5fec-140">Questa impostazione può essere configurata dalle impostazioni dell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="d5fec-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="d5fec-141">Nel Portale di Azure aprire l'app per la logica per cui si desidera aggiungere limitazioni per l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d5fec-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="d5fec-142">Fare clic sulla voce di menu **Access control configuration** (Configurazione controllo di accesso) in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5fec-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="d5fec-143">Specificare l'elenco di intervalli di indirizzi IP che devono essere accettati dal trigger.</span><span class="sxs-lookup"><span data-stu-id="d5fec-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="d5fec-144">Un intervallo IP valido assume il formato `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="d5fec-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="d5fec-145">Se si desidera che l'app per la logica venga attivata solo come app per la logica nidificata, selezionare l'opzione **Only other logic apps** (Solo altre app per la logica).</span><span class="sxs-lookup"><span data-stu-id="d5fec-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="d5fec-146">L'opzione scrive una matrice vuota nella risorsa; ciò significa che vengono attivate correttamente solo le chiamate dal servizio stesso (app per la logica padre).</span><span class="sxs-lookup"><span data-stu-id="d5fec-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="d5fec-147">Un'app per la logica con un trigger di richiesta potrebbe comunque essere eseguita tramite l'API REST/Gestione API `/triggers/{triggerName}/run` indipendentemente dall'IP.</span><span class="sxs-lookup"><span data-stu-id="d5fec-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="d5fec-148">In questo caso potrebbe essere richiesta l'autenticazione all'API REST di Azure e tutti gli eventi potrebbero essere visualizzati nel log di controllo di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5fec-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="d5fec-149">Impostare i criteri di controllo di accesso di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="d5fec-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="d5fec-150">Impostazione degli intervalli IP nella definizione della risorsa</span><span class="sxs-lookup"><span data-stu-id="d5fec-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="d5fec-151">Se si usa un [modello di distribuzione](logic-apps-create-deploy-template.md) per automatizzare le distribuzioni, le impostazioni dell'intervallo IP possono essere configurate nel modello risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5fec-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="d5fec-152">Aggiunta di Azure Active Directory, OAuth o altri standard di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d5fec-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="d5fec-153">Per aggiungere altri protocolli di autorizzazione a un'app per la logica, [Gestione API di Azure](https://azure.microsoft.com/services/api-management/) offre monitoraggio avanzato, sicurezza, criteri e documentazione per ogni endpoint in grado di esporre un'app per la logica come un'API.</span><span class="sxs-lookup"><span data-stu-id="d5fec-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="d5fec-154">Gestione API di Azure può esporre un endpoint privato o pubblico per l'app per la logica, che potrebbe sfruttare Azure Active Directory, certificati, OAuth o altri standard di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5fec-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="d5fec-155">Quando viene ricevuta una richiesta, Gestione API di Azure la inoltra all'app per la logica (eseguendo eventuali trasformazioni e restrizioni necessarie in transito).</span><span class="sxs-lookup"><span data-stu-id="d5fec-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="d5fec-156">È possibile usare le impostazioni dell'intervallo IP in ingresso nell'app per la logica per consentire il trigger solo da Gestione API.</span><span class="sxs-lookup"><span data-stu-id="d5fec-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="d5fec-157">Proteggere l'accesso per gestire o modificare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="d5fec-158">È possibile limitare l'accesso alle operazioni di gestione in un'app per la logica in modo che le operazioni sulla risorsa possano essere eseguite solo da utenti o gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="d5fec-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="d5fec-159">Le app per la logica usano la funzionalità di [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-configure.md) e possono essere personalizzate con gli stessi strumenti.</span><span class="sxs-lookup"><span data-stu-id="d5fec-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="d5fec-160">Esistono anche alcuni ruoli predefiniti a cui è possibile assegnare i membri della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="d5fec-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="d5fec-161">**Collaboratore per app per la logica**: offre l'accesso per visualizzare, modificare e aggiornare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d5fec-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="d5fec-162">Non è possibile rimuovere la risorsa o eseguire operazioni di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d5fec-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="d5fec-163">**Operatore per app per la logica**: può visualizzare l'app per la logica e la cronologia delle esecuzioni e abilitare o disabilitare.</span><span class="sxs-lookup"><span data-stu-id="d5fec-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="d5fec-164">Non è possibile modificare o aggiornare la definizione.</span><span class="sxs-lookup"><span data-stu-id="d5fec-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="d5fec-165">È inoltre possibile usare i [blocchi per le risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md) per impedire la modifica o l'eliminazione delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d5fec-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="d5fec-166">Questo risulta utile per evitare la modifica o l'eliminazione delle risorse di produzione.</span><span class="sxs-lookup"><span data-stu-id="d5fec-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="d5fec-167">Proteggere l'accesso ai contenuti della cronologia delle esecuzioni</span><span class="sxs-lookup"><span data-stu-id="d5fec-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="d5fec-168">È possibile limitare l'accesso ai contenuti di input o output dalle esecuzioni precedenti a intervalli di indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="d5fec-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="d5fec-169">Tutti i dati all'interno di un'esecuzione del flusso di lavoro è crittografata in transito e a riposo.</span><span class="sxs-lookup"><span data-stu-id="d5fec-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="d5fec-170">Quando viene effettuata una chiamata alla cronologia delle esecuzioni, il servizio autentica la richiesta e offre collegamenti alla richiesta, oltre a input e output di risposta.</span><span class="sxs-lookup"><span data-stu-id="d5fec-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="d5fec-171">Questo collegamento può essere protetto in modo che i contenuti vengano restituiti solo dalle richieste di visualizzare contenuto da un intervallo di indirizzi IP designato.</span><span class="sxs-lookup"><span data-stu-id="d5fec-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="d5fec-172">È possibile usare questa funzionalità per il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="d5fec-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="d5fec-173">È anche possibile specificare un indirizzo IP come `0.0.0.0` in modo che nessuno possa accedere a input e output.</span><span class="sxs-lookup"><span data-stu-id="d5fec-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="d5fec-174">Questa restrizione può essere rimossa solo da qualcuno con autorizzazioni di amministratore per offrire l'accesso "just-in-time" ai contenuti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d5fec-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="d5fec-175">Questa impostazione può essere configurata nelle impostazioni della risorsa del Portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="d5fec-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="d5fec-176">Nel Portale di Azure aprire l'app per la logica per cui si desidera aggiungere limitazioni per l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d5fec-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="d5fec-177">Fare clic sulla voce di menu **Access control configuration** (Configurazione controllo di accesso) in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5fec-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="d5fec-178">Specificare l'elenco di intervalli di indirizzi IP per l'accesso al contenuto</span><span class="sxs-lookup"><span data-stu-id="d5fec-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="d5fec-179">Impostazione degli intervalli IP nella definizione della risorsa</span><span class="sxs-lookup"><span data-stu-id="d5fec-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="d5fec-180">Se si usa un [modello di distribuzione](logic-apps-create-deploy-template.md) per automatizzare le distribuzioni, le impostazioni dell'intervallo IP possono essere configurate nel modello risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5fec-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="d5fec-181">Proteggere i parametri e gli input all'interno di un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="d5fec-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="d5fec-182">Esistono alcuni aspetti della definizione di un flusso di lavoro per cui potrebbe essere opportuno creare parametri per la distribuzione nei diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="d5fec-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="d5fec-183">Inoltre, alcuni di questi parametri potrebbero essere parametri protetti da non visualizzare durante la modifica di un flusso di lavoro, ad esempio un ID client e un segreto client per [l'autenticazione di Azure Active Directory](../connectors/connectors-native-http.md#authentication) di un'azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5fec-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="d5fec-184">Uso di parametri e parametri protetti</span><span class="sxs-lookup"><span data-stu-id="d5fec-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="d5fec-185">Il [linguaggio di definizione del flusso di lavoro](http://aka.ms/logicappsdocs) assicura un'operazione `@parameters()` per accedere al valore di un parametro di risorsa in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="d5fec-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="d5fec-186">È inoltre possibile [specificare parametri nel modello di distribuzione risorse](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="d5fec-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="d5fec-187">Se si specifica un tipo di parametro come `securestring`, questo non verrà restituito con il resto della definizione della risorsa, ovvero non sarà accessibile visualizzando la risorsa dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d5fec-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="d5fec-188">Se il parametro viene usato nelle intestazioni o nel corpo della richiesta, potrebbe essere visibile accedendo alla cronologia delle esecuzioni e alla richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="d5fec-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="d5fec-189">Assicurarsi di configurare di conseguenza i criteri di accesso ai contenuti.</span><span class="sxs-lookup"><span data-stu-id="d5fec-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="d5fec-190">Le intestazioni di autorizzazione non sono mai visibili tramite input o output.</span><span class="sxs-lookup"><span data-stu-id="d5fec-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="d5fec-191">Pertanto, se usato in tale contesto, il segreto non è recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5fec-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="d5fec-192">Modello di distribuzione risorse con segreti</span><span class="sxs-lookup"><span data-stu-id="d5fec-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="d5fec-193">Di seguito è riportato un esempio di distribuzione che fa riferimento a un parametro protetto di `secret` in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="d5fec-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="d5fec-194">In un file di parametri separato è possibile specificare il valore dell'ambiente per `secret` oppure sfruttare l'[insieme di credenziali delle chiavi di Azure Resource Manager](../azure-resource-manager/resource-manager-keyvault-parameter.md) per recuperare i segreti in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d5fec-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="d5fec-195">Proteggere l'accesso ai servizi che ricevono richieste da un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="d5fec-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="d5fec-196">Esistono diversi modi per proteggere qualsiasi endpoint a cui l'app per la logica deve accedere.</span><span class="sxs-lookup"><span data-stu-id="d5fec-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="d5fec-197">Uso dell'autenticazione nelle richieste in uscita</span><span class="sxs-lookup"><span data-stu-id="d5fec-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="d5fec-198">Quando si lavora con un'azione HTTP, HTTP + Swagger (Open API) o Webhook, è possibile aggiungere l'autenticazione alla richiesta inviata.</span><span class="sxs-lookup"><span data-stu-id="d5fec-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="d5fec-199">Potrebbe trattarsi di autenticazione di base, autenticazione del certificato o l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5fec-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="d5fec-200">Informazioni dettagliate su come configurare l'autenticazione sono disponibili [in questo articolo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="d5fec-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="d5fec-201">Limitazione dell'accesso agli indirizzi IP delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="d5fec-202">Tutte le chiamate dalle app per la logica provengono da un set specifico di indirizzi IP in base all'area.</span><span class="sxs-lookup"><span data-stu-id="d5fec-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="d5fec-203">È possibile aggiungere altri filtri in modo da accettare solo richieste da tali indirizzi IP designati.</span><span class="sxs-lookup"><span data-stu-id="d5fec-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="d5fec-204">Per un elenco di indirizzi IP, vedere [Limiti e configurazione delle app per la logica](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="d5fec-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="d5fec-205">Connettività locale</span><span class="sxs-lookup"><span data-stu-id="d5fec-205">On-premises connectivity</span></span>

<span data-ttu-id="d5fec-206">Le app per la logica offrono integrazione con numerosi servizi per garantire una comunicazione locale sicura e affidabile.</span><span class="sxs-lookup"><span data-stu-id="d5fec-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="d5fec-207">Gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="d5fec-207">On-premises data gateway</span></span>

<span data-ttu-id="d5fec-208">Molti dei connettori gestiti delle app per la logica offrono una connettività sicura a sistemi locali, tra cui File System, SQL, SharePoint, DB2 e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="d5fec-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="d5fec-209">Il gateway inoltra i dati da origini locali sui canali crittografati tramite il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5fec-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="d5fec-210">Tutto il traffico ha origine come traffico sicuro in uscita dall'agente di gateway.</span><span class="sxs-lookup"><span data-stu-id="d5fec-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="d5fec-211">Altre informazioni sul [funzionamento del gateway dati](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="d5fec-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="d5fec-212">Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="d5fec-212">Azure API Management</span></span>

<span data-ttu-id="d5fec-213">[Gestione API di Azure](https://azure.microsoft.com/services/api-management/) dispone di numerose opzioni di connettività locale, tra cui l'integrazione ExpressRoute e VPN da sito a sito per la protezione del proxy e la comunicazione con i sistemi locali.</span><span class="sxs-lookup"><span data-stu-id="d5fec-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="d5fec-214">Nella finestra di progettazione delle app per la logica è possibile selezionare rapidamente un'API esposta da Gestione API di Azure all'interno di un flusso di lavoro, in modo da offrire accesso rapido ai sistemi locali.</span><span class="sxs-lookup"><span data-stu-id="d5fec-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="d5fec-215">Connessioni ibride dai servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="d5fec-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="d5fec-216">È possibile usare la funzionalità di connessione ibrida locale per consentire la comunicazione tra l'API di Azure e le App Web.</span><span class="sxs-lookup"><span data-stu-id="d5fec-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="d5fec-217">Informazioni dettagliate sulle connessioni ibride e su come configurarle sono disponibili [in questo articolo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5fec-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5fec-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5fec-218">Next steps</span></span>
[<span data-ttu-id="d5fec-219">Creare un modello di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d5fec-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="d5fec-220">Gestione delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="d5fec-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="d5fec-221">Monitorare le app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="d5fec-222">Diagnosi degli errori delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="d5fec-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
