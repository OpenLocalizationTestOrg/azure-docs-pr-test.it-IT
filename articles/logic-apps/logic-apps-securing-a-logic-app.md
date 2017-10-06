---
title: aaaSecure di accedere alle app di logica tooAzure | Documenti Microsoft
description: Aggiunta di sicurezza per la protezione di accesso tootriggers, input e output, i parametri di azione e servizi utilizzati con i flussi di lavoro in Azure App per la logica.
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
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="60d18-103">Proteggere l'accesso alle App per la logica tooyour</span><span class="sxs-lookup"><span data-stu-id="60d18-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="60d18-104">Esistono toohelp disponibili molti strumenti di proteggere le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="60d18-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="60d18-105">Protezione accesso tootrigger un'app di logica (Trigger di richiesta HTTP)</span><span class="sxs-lookup"><span data-stu-id="60d18-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="60d18-106">Protezione accesso toomanage, modificare o leggere un'app di logica</span><span class="sxs-lookup"><span data-stu-id="60d18-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="60d18-107">Protezione accesso toocontents di input e output per un'esecuzione</span><span class="sxs-lookup"><span data-stu-id="60d18-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="60d18-108">Protezione di parametri o input all'interno di azioni in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="60d18-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="60d18-109">Protezione accesso tooservices che ricevono richieste da un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="60d18-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="60d18-110">Accesso sicuro tootrigger</span><span class="sxs-lookup"><span data-stu-id="60d18-110">Secure access tootrigger</span></span>

<span data-ttu-id="60d18-111">Quando si lavora con un'app di logica che viene attivato su una richiesta HTTP ([richiesta](../connectors/connectors-native-reqres.md) o [Webhook](../connectors/connectors-native-webhook.md)), è possibile limitare l'accesso in modo che solo i client autorizzati possono essere attivati hello logica app.</span><span class="sxs-lookup"><span data-stu-id="60d18-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="60d18-112">Tutte le richieste in un'app per la logica vengono crittografate e protette tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="60d18-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="60d18-113">Firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="60d18-113">Shared Access Signature</span></span>

<span data-ttu-id="60d18-114">Ogni endpoint di richiesta per un'app logica include un [firma di accesso condiviso (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) come parte dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="60d18-115">Ogni URL contiene parametri di query `sp`, `sv` e `sig`.</span><span class="sxs-lookup"><span data-stu-id="60d18-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="60d18-116">Le autorizzazioni sono specificate dai `sp`, e i corrispondenti metodi tooHTTP consentiti, `sv` è toogenerate versione utilizzata hello, e `sig` è tootrigger accesso tooauthenticate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="60d18-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="60d18-117">firma Hello viene generato utilizzando l'algoritmo SHA256 hello con una chiave segreta in tutti i percorsi URL hello e proprietà.</span><span class="sxs-lookup"><span data-stu-id="60d18-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="60d18-118">chiave segreta Hello viene mai esposta e pubblicata e vengono mantenute crittografate e archiviate come parte di app per la logica hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="60d18-119">App logica autorizza solo i trigger che include una firma valida creata con la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="60d18-120">Per rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="60d18-120">Regenerate access keys</span></span>

<span data-ttu-id="60d18-121">È possibile rigenerare una chiave protetta nuovo a in qualsiasi momento tramite il portale di Azure o di API REST hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="60d18-122">Tutti gli URL correnti che sono stati generati in precedenza utilizzando la chiave precedente hello sono toofire invalidato e non è più autorizzato hello logica app.</span><span class="sxs-lookup"><span data-stu-id="60d18-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="60d18-123">Nel portale di Azure hello, aprire hello logica app da tooregenerate una chiave</span><span class="sxs-lookup"><span data-stu-id="60d18-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="60d18-124">Fare clic su hello **chiavi di accesso** voce di menu in **impostazioni**</span><span class="sxs-lookup"><span data-stu-id="60d18-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="60d18-125">Scegliere tooregenerate chiave hello e processo hello completo</span><span class="sxs-lookup"><span data-stu-id="60d18-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="60d18-126">URL recuperate dopo la rigenerazione sono firmati con una nuova chiave di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="60d18-127">Creazione di URL di callback con una data di scadenza</span><span class="sxs-lookup"><span data-stu-id="60d18-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="60d18-128">Se si condivide hello URL con altre parti, è possibile generare gli URL con chiavi specifiche e le date di scadenza in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="60d18-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="60d18-129">È possibile quindi facilmente distribuire le chiavi o garantire accesso toofire un'app è limitato tooa determinati timespan.</span><span class="sxs-lookup"><span data-stu-id="60d18-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="60d18-130">È possibile specificare una data di scadenza per un URL tramite hello [App API REST per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="60d18-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="60d18-131">Nel corpo di hello, includere proprietà hello `NotAfter` come stringa di data JSON, che restituisce un URL di callback che è valido solo fino a quando hello `NotAfter` data e ora.</span><span class="sxs-lookup"><span data-stu-id="60d18-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="60d18-132">Creazione di URL con una chiave privata primaria o secondaria</span><span class="sxs-lookup"><span data-stu-id="60d18-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="60d18-133">Quando si genera o elenco di URL callback per i trigger basata su richiesta, è possibile specificare anche l'URL hello toosign toouse chiave.</span><span class="sxs-lookup"><span data-stu-id="60d18-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="60d18-134">È possibile generare un URL firmato da una chiave specifica tramite hello [App API REST per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="60d18-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="60d18-135">Nel corpo di hello, includere proprietà hello `KeyType` come `Primary` o `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="60d18-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="60d18-136">Restituisce un URL firmato dalla chiave di hello sicuro specificata.</span><span class="sxs-lookup"><span data-stu-id="60d18-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="60d18-137">Limitare gli indirizzi IP in ingresso</span><span class="sxs-lookup"><span data-stu-id="60d18-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="60d18-138">Inoltre toohello firma di accesso condiviso, è preferibile toorestrict la chiamata di un'app logica solo da un client specifico.</span><span class="sxs-lookup"><span data-stu-id="60d18-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="60d18-139">Ad esempio, se si gestisce l'endpoint tramite Gestione API di Azure, è possibile limitare la logica di hello tooonly app accettare la richiesta di hello quando hello richiesta proviene da hello indirizzo IP dell'istanza gestione API.</span><span class="sxs-lookup"><span data-stu-id="60d18-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="60d18-140">Questa impostazione può essere configurata all'interno delle impostazioni di hello logica app:</span><span class="sxs-lookup"><span data-stu-id="60d18-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="60d18-141">Nel portale di Azure hello, aprire hello logica app da tooadd restrizioni degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="60d18-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="60d18-142">Fare clic su hello **configurazione di controllo di accesso** voce di menu in **impostazioni**</span><span class="sxs-lookup"><span data-stu-id="60d18-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="60d18-143">Specificare elenco hello di toobe gli intervalli di indirizzi IP accettati dal trigger hello</span><span class="sxs-lookup"><span data-stu-id="60d18-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="60d18-144">Un intervallo IP valido ha il formato di hello `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="60d18-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="60d18-145">Se si desidera hello logica app tooonly incendio come app nidificata logica, selezionare hello **solo ad altre App logica** opzione.</span><span class="sxs-lookup"><span data-stu-id="60d18-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="60d18-146">Questa opzione consente di scrivere una risorsa toohello matrice vuota, ovvero solo le chiamate da hello servizio stesso (padre logica App) attivati correttamente.</span><span class="sxs-lookup"><span data-stu-id="60d18-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="60d18-147">È comunque possibile eseguire un'app logica con un trigger di richiesta tramite l'API REST hello / gestione `/triggers/{triggerName}/run` indipendentemente dall'IP.</span><span class="sxs-lookup"><span data-stu-id="60d18-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="60d18-148">Questo scenario richiede l'autenticazione di base hello API REST di Azure e tutti gli eventi verrebbero visualizzati nella hello Log di controllo di Azure.</span><span class="sxs-lookup"><span data-stu-id="60d18-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="60d18-149">Impostare i criteri di controllo di accesso di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="60d18-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="60d18-150">L'impostazione di intervalli IP nella definizione di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="60d18-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="60d18-151">Se si utilizza un [modello di distribuzione](logic-apps-create-deploy-template.md) tooautomate le distribuzioni, le impostazioni dell'intervallo IP hello possono essere configurate nel modello di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="60d18-152">Aggiunta di Azure Active Directory, OAuth o altri standard di sicurezza</span><span class="sxs-lookup"><span data-stu-id="60d18-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="60d18-153">autorizzazione più protocolli nella parte superiore di un'app di logica, tooadd [gestione API di Azure](https://azure.microsoft.com/services/api-management/) offre una app come un'API per la logica di monitoraggio, protezione, criteri e la documentazione per un endpoint con tooexpose funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="60d18-154">Gestione API di Azure possono esporre un endpoint pubblico o privato per hello logica app, che può usare Azure Active Directory, certificato, OAuth o altri standard di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="60d18-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="60d18-155">Quando viene ricevuta una richiesta, gestione API di Azure inoltra hello richiesta toohello logica app (esecuzione di eventuali trasformazioni necessarie o restrizioni in transito).</span><span class="sxs-lookup"><span data-stu-id="60d18-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="60d18-156">È possibile utilizzare l'intervallo IP in ingresso hello impostazioni hello logica app tooonly consentiranno hello logica app toobe attivato da Gestione API.</span><span class="sxs-lookup"><span data-stu-id="60d18-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="60d18-157">Proteggere l'accesso alle App per la logica toomanage o di modifica</span><span class="sxs-lookup"><span data-stu-id="60d18-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="60d18-158">È possibile limitare l'accesso toomanagement operazioni su un'app logica in modo che solo utenti o gruppi specifici siano in grado di tooperform operazioni sulla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="60d18-159">App per la logica di utilizzare hello Azure [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) funzionalità e può essere personalizzata con hello stessi strumenti.</span><span class="sxs-lookup"><span data-stu-id="60d18-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="60d18-160">Esistono alcuni ruoli predefiniti, che è possibile assegnare anche i membri di tooas la sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="60d18-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="60d18-161">**Logica App collaboratore** -fornisce accesso tooview, modificare e aggiornare un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="60d18-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="60d18-162">Impossibile rimuovere la risorsa hello o eseguire operazioni di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="60d18-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="60d18-163">**Logica App operatore** : può visualizzare hello logica app e la cronologia di esecuzione e abilitare o disabilitare.</span><span class="sxs-lookup"><span data-stu-id="60d18-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="60d18-164">Non è possibile modificare o aggiornare la definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="60d18-165">È inoltre possibile utilizzare [il blocco di risorsa di Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent modifica o eliminazione di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="60d18-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="60d18-166">Questa funzionalità è utile tooprevent risorse di produzione da modifiche o eliminazioni.</span><span class="sxs-lookup"><span data-stu-id="60d18-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="60d18-167">Accesso sicuro toocontents di hello cronologia di esecuzione</span><span class="sxs-lookup"><span data-stu-id="60d18-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="60d18-168">È possibile limitare l'accesso toocontents di input o output da precedenti esecuzioni toospecific intervalli di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="60d18-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="60d18-169">Tutti i dati all'interno di un'esecuzione del flusso di lavoro è crittografata in transito e a riposo.</span><span class="sxs-lookup"><span data-stu-id="60d18-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="60d18-170">Quando viene effettuata una cronologia toorun chiamata, il servizio di hello autentica hello richiesta e fornisce collegamenti toohello richiesta e di input di risposta e di output.</span><span class="sxs-lookup"><span data-stu-id="60d18-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="60d18-171">Questo collegamento può essere protette richieste pertanto sola tooview contenuto da un intervallo di indirizzi IP designato restituiscono contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="60d18-172">È possibile usare questa funzionalità per il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="60d18-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="60d18-173">È anche possibile specificare un indirizzo IP come `0.0.0.0` in modo che nessuno possa accedere a input e output.</span><span class="sxs-lookup"><span data-stu-id="60d18-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="60d18-174">È necessario disporre delle autorizzazioni di amministratore è stato possibile rimuovere questa restrizione, fornendo il possibilità hello per contenuto tooworkflow 'just-in-time' accesso.</span><span class="sxs-lookup"><span data-stu-id="60d18-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="60d18-175">Questa impostazione può essere configurata all'interno delle impostazioni risorsa hello hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="60d18-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="60d18-176">Nel portale di Azure hello, aprire hello logica app da tooadd restrizioni degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="60d18-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="60d18-177">Fare clic su hello **configurazione di controllo di accesso** voce di menu in **impostazioni**</span><span class="sxs-lookup"><span data-stu-id="60d18-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="60d18-178">Specificare elenco hello di intervalli di indirizzi IP per l'accesso toocontent</span><span class="sxs-lookup"><span data-stu-id="60d18-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="60d18-179">L'impostazione di intervalli IP nella definizione di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="60d18-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="60d18-180">Se si utilizza un [modello di distribuzione](logic-apps-create-deploy-template.md) tooautomate le distribuzioni, le impostazioni dell'intervallo IP hello possono essere configurate nel modello di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="60d18-181">Proteggere i parametri e gli input all'interno di un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="60d18-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="60d18-182">È possibile tooparameterize alcuni aspetti di una definizione del flusso di lavoro per la distribuzione tra ambienti.</span><span class="sxs-lookup"><span data-stu-id="60d18-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="60d18-183">Inoltre, alcuni parametri potrebbero essere parametri protetti non si desidera tooappear durante la modifica di un flusso di lavoro, ad esempio un ID client e segreto client per [l'autenticazione di Azure Active Directory](../connectors/connectors-native-http.md#authentication) di un'azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="60d18-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="60d18-184">Uso di parametri e parametri protetti</span><span class="sxs-lookup"><span data-stu-id="60d18-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="60d18-185">tooaccess hello valore di un parametro di risorsa in fase di esecuzione, hello [il linguaggio di definizione del flusso di lavoro](http://aka.ms/logicappsdocs) fornisce un `@parameters()` operazione.</span><span class="sxs-lookup"><span data-stu-id="60d18-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="60d18-186">Inoltre, è possibile [specificare i parametri nel modello di distribuzione di risorse hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="60d18-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="60d18-187">Ma se si specifica il tipo di parametro hello come `securestring`, non viene restituito con il resto di hello hello della definizione di risorsa, il parametro hello e non saranno accessibile da Visualizzazione risorse hello dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="60d18-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="60d18-188">Se il parametro viene utilizzato in intestazioni hello o il corpo di una richiesta, il parametro hello potrebbe essere visibile mediante l'accesso alla cronologia di esecuzione hello e richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="60d18-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="60d18-189">Verificare che tooset i criteri di accesso al contenuto di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="60d18-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="60d18-190">Le intestazioni di autorizzazione non sono mai visibili tramite input o output.</span><span class="sxs-lookup"><span data-stu-id="60d18-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="60d18-191">Se viene utilizzato il segreto hello sono, segreto hello non è recuperabile.</span><span class="sxs-lookup"><span data-stu-id="60d18-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="60d18-192">Modello di distribuzione risorse con segreti</span><span class="sxs-lookup"><span data-stu-id="60d18-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="60d18-193">Hello esempio seguente viene illustrata una distribuzione che fa riferimento a un parametro di secure `secret` in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="60d18-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="60d18-194">In un file di parametri separati, è possibile specificare il valore di ambiente hello per hello `secret`, oppure utilizzare [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segreti al momento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="60d18-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

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
                "body": "This is hello request"
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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="60d18-195">Proteggere l'accesso alle richieste di ricezione tooservices da un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="60d18-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="60d18-196">Esistono molti modi toohelp qualsiasi app per la logica hello endpoint deve tooaccess sicura.</span><span class="sxs-lookup"><span data-stu-id="60d18-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="60d18-197">Uso dell'autenticazione nelle richieste in uscita</span><span class="sxs-lookup"><span data-stu-id="60d18-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="60d18-198">Quando si lavora con un HTTP, HTTP + Swagger (API aperta) o azione Webhook, è possibile aggiungere una richiesta di autenticazione toohello inviato.</span><span class="sxs-lookup"><span data-stu-id="60d18-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="60d18-199">Potrebbe trattarsi di autenticazione di base, autenticazione del certificato o l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60d18-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="60d18-200">Informazioni dettagliate su come tooconfigure questa autenticazione è reperibile [in questo articolo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="60d18-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="60d18-201">Limitazione degli indirizzi IP di accesso toologic app</span><span class="sxs-lookup"><span data-stu-id="60d18-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="60d18-202">Tutte le chiamate dalle app per la logica provengono da un set specifico di indirizzi IP in base all'area.</span><span class="sxs-lookup"><span data-stu-id="60d18-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="60d18-203">È possibile aggiungere ulteriori filtri tooonly accetta richieste da quelli indicati gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="60d18-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="60d18-204">Per un elenco di indirizzi IP, vedere [Limiti e configurazione delle app per la logica](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="60d18-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="60d18-205">Connettività locale</span><span class="sxs-lookup"><span data-stu-id="60d18-205">On-premises connectivity</span></span>

<span data-ttu-id="60d18-206">App per la logica forniscono l'integrazione con diversi servizi tooprovide, sicuro e affidabile la comunicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="60d18-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="60d18-207">Gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="60d18-207">On-premises data gateway</span></span>

<span data-ttu-id="60d18-208">Molti connettori gestiti per App per la logica forniscono una connettività sicura sistemi tooon locali, inclusi File System, SQL, SharePoint, DB2 e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="60d18-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="60d18-209">gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="60d18-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="60d18-210">Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello.</span><span class="sxs-lookup"><span data-stu-id="60d18-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="60d18-211">Altre informazioni, vedere [funzionamento gateway dati hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="60d18-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="60d18-212">Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="60d18-212">Azure API Management</span></span>

<span data-ttu-id="60d18-213">[Gestione API di Azure](https://azure.microsoft.com/services/api-management/) sono disponibili opzioni di connettività locale, inclusa l'integrazione di ExpressRoute e VPN da sito a sito per i sistemi locali tooon proxy e comunicazione protetti.</span><span class="sxs-lookup"><span data-stu-id="60d18-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="60d18-214">Nella finestra di progettazione logica App hello, è possibile selezionare rapidamente un'API esposta da Gestione API di Azure all'interno di un flusso di lavoro forniscono un rapido accesso sistemi tooon locali.</span><span class="sxs-lookup"><span data-stu-id="60d18-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="60d18-215">Connessioni ibride dai servizi app di Azure</span><span class="sxs-lookup"><span data-stu-id="60d18-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="60d18-216">È possibile utilizzare funzionalità di una connessione ibrida locale hello per le API di Azure e Web App toocommunicate locale.</span><span class="sxs-lookup"><span data-stu-id="60d18-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="60d18-217">Informazioni dettagliate sulle connessioni ibride e come è possibile trovare tooconfigure [in questo articolo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="60d18-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60d18-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60d18-218">Next steps</span></span>
[<span data-ttu-id="60d18-219">Creare un modello di distribuzione</span><span class="sxs-lookup"><span data-stu-id="60d18-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="60d18-220">Gestione delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="60d18-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="60d18-221">Monitorare le app per la logica</span><span class="sxs-lookup"><span data-stu-id="60d18-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="60d18-222">Diagnosi degli errori delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="60d18-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
