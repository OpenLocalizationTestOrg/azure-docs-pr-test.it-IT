---
title: Panoramica del modello di sicurezza e autenticazione di Hub eventi di Azure | Documentazione Microsoft
description: Panoramica sul modello di autenticazione e sicurezza di Hub eventi.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="d48ce-103">Panoramica sull’autenticazione di Hub eventi e sul modello di protezione</span><span class="sxs-lookup"><span data-stu-id="d48ce-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="d48ce-104">Il modello di sicurezza di Hub eventi di Azure soddisfa i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d48ce-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="d48ce-105">Solo i client che presentano le credenziali valide possono inviare dati a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="d48ce-106">Un client non può rappresentare un altro client.</span><span class="sxs-lookup"><span data-stu-id="d48ce-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="d48ce-107">A un client non autorizzato può essere impedito l'invio di dati a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="d48ce-108">Autenticazione client</span><span class="sxs-lookup"><span data-stu-id="d48ce-108">Client authentication</span></span>
<span data-ttu-id="d48ce-109">Il modello di sicurezza di Hub eventi si basa su una combinazione di token di [firma di accesso condiviso](../service-bus-messaging/service-bus-sas.md) e *autori di eventi*.</span><span class="sxs-lookup"><span data-stu-id="d48ce-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="d48ce-110">Un autore di eventi definisce un endpoint virtuale per un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="d48ce-111">L'autore è utilizzabile solo per inviare messaggi a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="d48ce-112">Non è possibile ricevere messaggi da un autore.</span><span class="sxs-lookup"><span data-stu-id="d48ce-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="d48ce-113">In genere, un Hub eventi usa un autore per ogni client.</span><span class="sxs-lookup"><span data-stu-id="d48ce-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="d48ce-114">Tutti i messaggi inviati a uno qualsiasi degli autori di un Hub eventi vengono accodati all'interno di tale Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="d48ce-115">Gli autori consentono la limitazione e il controllo di accesso con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="d48ce-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="d48ce-116">A ogni client di Hub eventi viene assegnato un token univoco, che viene caricato nel client.</span><span class="sxs-lookup"><span data-stu-id="d48ce-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="d48ce-117">I token vengono prodotti in modo tale che ogni token univoco conceda l'accesso a un diverso autore univoco.</span><span class="sxs-lookup"><span data-stu-id="d48ce-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="d48ce-118">Un client che possiede un token può inviare a un solo autore e a nessun altro autore.</span><span class="sxs-lookup"><span data-stu-id="d48ce-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="d48ce-119">Se più client condividono lo stesso token, ognuno di essi condivide un autore.</span><span class="sxs-lookup"><span data-stu-id="d48ce-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="d48ce-120">Sebbene non sia consigliato, è possibile dotare i dispositivi di token che concedono l'accesso diretto a un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="d48ce-121">Qualsiasi dispositivo che contiene un token di questo tipo può inviare messaggi direttamente a tale hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="d48ce-122">Tale dispositivo non sarà soggetto alla limitazione.</span><span class="sxs-lookup"><span data-stu-id="d48ce-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="d48ce-123">Non è possibile disattivare l'invio a tale Hub eventi per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d48ce-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="d48ce-124">Tutti i token sono firmati con una chiave SAS.</span><span class="sxs-lookup"><span data-stu-id="d48ce-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="d48ce-125">In genere, tutti i token sono firmati con la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="d48ce-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="d48ce-126">I client non conoscono la chiave, per cui altri client non possono produrre token.</span><span class="sxs-lookup"><span data-stu-id="d48ce-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="d48ce-127">Creare la chiave SAS</span><span class="sxs-lookup"><span data-stu-id="d48ce-127">Create the SAS key</span></span>

<span data-ttu-id="d48ce-128">Quando si crea uno spazio dei nomi di Hub eventi, il servizio genera una chiave di firma di accesso condiviso a 256 bit denominata **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="d48ce-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="d48ce-129">Tale chiave concede diritti di invio, attesa e gestione allo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="d48ce-130">È anche possibile creare chiavi aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d48ce-130">You can also create additional keys.</span></span> <span data-ttu-id="d48ce-131">Si consiglia di produrre una chiave che concede le autorizzazioni di invio allo specifico Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="d48ce-132">Nella parte restante di questo argomento si presuppone che questa chiave sia denominata **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="d48ce-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="d48ce-133">Nell'esempio seguente viene creata una chiave di solo invio durante la creazione dell'Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="d48ce-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="d48ce-134">Generare token</span><span class="sxs-lookup"><span data-stu-id="d48ce-134">Generate tokens</span></span>

<span data-ttu-id="d48ce-135">È possibile generare token utilizzando la chiave SAS.</span><span class="sxs-lookup"><span data-stu-id="d48ce-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="d48ce-136">È necessario ottenere solo un token per client.</span><span class="sxs-lookup"><span data-stu-id="d48ce-136">You must produce only one token per client.</span></span> <span data-ttu-id="d48ce-137">È possibile produrre token utilizzando il metodo riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d48ce-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="d48ce-138">Tutti i token vengono generati utilizzando la chiave **EventHubSendKey** .</span><span class="sxs-lookup"><span data-stu-id="d48ce-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="d48ce-139">A ogni token viene assegnato un URI univoco.</span><span class="sxs-lookup"><span data-stu-id="d48ce-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="d48ce-140">Quando si chiama questo metodo, l'URI deve essere specificato come `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="d48ce-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="d48ce-141">Per tutti i token l'URI è identico, ad eccezione di `PUBLISHER_NAME`, che deve essere diverso per ogni token.</span><span class="sxs-lookup"><span data-stu-id="d48ce-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="d48ce-142">In teoria, `PUBLISHER_NAME` rappresenta l'ID del client che riceve il token.</span><span class="sxs-lookup"><span data-stu-id="d48ce-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="d48ce-143">Questo metodo genera un token con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="d48ce-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="d48ce-144">L'ora di scadenza del token è espressa in secondi dal 1 gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="d48ce-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="d48ce-145">Di seguito è riportato un esempio di token:</span><span class="sxs-lookup"><span data-stu-id="d48ce-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="d48ce-146">In genere, i token hanno una durata simile o superiore a quella del client.</span><span class="sxs-lookup"><span data-stu-id="d48ce-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="d48ce-147">Se il client è in grado di ottenere un nuovo token, è possibile usare token con una durata più breve.</span><span class="sxs-lookup"><span data-stu-id="d48ce-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="d48ce-148">Invio di dati</span><span class="sxs-lookup"><span data-stu-id="d48ce-148">Sending data</span></span>
<span data-ttu-id="d48ce-149">Dopo avere creato i token, viene eseguito il provisioning di ogni client con il proprio token univoco.</span><span class="sxs-lookup"><span data-stu-id="d48ce-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="d48ce-150">Quando il client invia dati a un hub eventi, contrassegna la richiesta di invio con il token.</span><span class="sxs-lookup"><span data-stu-id="d48ce-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="d48ce-151">Per evitare che un utente malintenzionato intercetti e rubi il token, la comunicazione tra il client e l'Hub eventi deve verificarsi su un canale crittografato.</span><span class="sxs-lookup"><span data-stu-id="d48ce-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="d48ce-152">Disattivazione dei client</span><span class="sxs-lookup"><span data-stu-id="d48ce-152">Blacklisting clients</span></span>
<span data-ttu-id="d48ce-153">In caso di furto di un token da parte di un utente malintenzionato, l'autore dell'attacco può rappresentare il client il cui token è stato rubato.</span><span class="sxs-lookup"><span data-stu-id="d48ce-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="d48ce-154">La disattivazione di un client rende il rendering di tale client inutilizzabile fino a che non riceve un nuovo token che usa un autore diverso.</span><span class="sxs-lookup"><span data-stu-id="d48ce-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="d48ce-155">Autenticazione delle applicazioni back-end</span><span class="sxs-lookup"><span data-stu-id="d48ce-155">Authentication of back-end applications</span></span>

<span data-ttu-id="d48ce-156">Per autenticare le applicazioni back-end che usano i dati generati dai client di Hub eventi, Hub eventi usa un modello di sicurezza simile al modello usato per gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d48ce-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="d48ce-157">Un gruppo di consumer di Hub eventi equivale a una sottoscrizione a un argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d48ce-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="d48ce-158">Un client può creare un gruppo di consumer se la richiesta di creazione è accompagnata da un token che concede privilegi di gestione per l'hub eventi o per lo spazio dei nomi a cui appartiene l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="d48ce-159">Un client può usare dati di un gruppo di consumer se la richiesta di ricezione è accompagnata da un token che concede i diritti di ricezione in tale gruppo di consumer, l'Hub eventi o lo spazio dei nomi a cui appartiene l'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="d48ce-160">La versione corrente del bus di servizio non supporta regole di firma di accesso condiviso per sottoscrizioni singole.</span><span class="sxs-lookup"><span data-stu-id="d48ce-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="d48ce-161">Lo stesso vale per i gruppi di consumer di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="d48ce-162">In futuro verrà aggiunto il supporto SAS per entrambe le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d48ce-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="d48ce-163">In assenza di autenticazione SAS per gruppi di consumer singoli, è possibile utilizzare chiavi SAS per proteggere tutti i gruppi di consumer con una chiave comune.</span><span class="sxs-lookup"><span data-stu-id="d48ce-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="d48ce-164">Questo approccio consente a un'applicazione di usare dati di tutti i gruppi di consumer di un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d48ce-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d48ce-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d48ce-165">Next steps</span></span>
<span data-ttu-id="d48ce-166">Per altre informazioni su Hub eventi, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d48ce-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="d48ce-167">[Panoramica di Hub eventi]</span><span class="sxs-lookup"><span data-stu-id="d48ce-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="d48ce-168">[Panoramica delle firme di accesso condiviso]</span><span class="sxs-lookup"><span data-stu-id="d48ce-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="d48ce-169">[Applicazioni di esempio che usano Hub eventi]</span><span class="sxs-lookup"><span data-stu-id="d48ce-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="d48ce-170">[Panoramica di Hub eventi]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="d48ce-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="d48ce-171">[Applicazioni di esempio che usano Hub eventi]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="d48ce-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="d48ce-172">[Panoramica delle firme di accesso condiviso]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="d48ce-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

