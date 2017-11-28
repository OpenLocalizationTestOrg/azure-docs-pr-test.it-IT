---
title: aaaOverview del modello di autenticazione e sicurezza degli hub di eventi di Azure | Documenti Microsoft
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
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="9aeb1-103">Panoramica sull’autenticazione di Hub eventi e sul modello di protezione</span><span class="sxs-lookup"><span data-stu-id="9aeb1-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="9aeb1-104">modello di sicurezza degli hub di eventi di Azure Hello soddisfa hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="9aeb1-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="9aeb1-105">Solo i client che presentano credenziali valide possono inviare hub eventi tooan di dati.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="9aeb1-106">Un client non può rappresentare un altro client.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="9aeb1-107">Un client non autorizzato può essere bloccato per l'invio di hub di eventi tooan di dati.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="9aeb1-108">Autenticazione client</span><span class="sxs-lookup"><span data-stu-id="9aeb1-108">Client authentication</span></span>
<span data-ttu-id="9aeb1-109">modello di sicurezza degli hub eventi Hello è basato su una combinazione di [firma di accesso condiviso (SAS)](../service-bus-messaging/service-bus-sas.md) token e *i Publisher di eventi*.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="9aeb1-110">Un autore di eventi definisce un endpoint virtuale per un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="9aeb1-111">server di pubblicazione Hello può essere solo hub di eventi tooan messaggi toosend utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="9aeb1-112">Non è possibile tooreceive messaggi da un server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="9aeb1-113">In genere, un Hub eventi usa un autore per ogni client.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="9aeb1-114">Tutti i messaggi vengono inviati tooany degli editori di hello di un hub eventi vengono accodati all'interno di tale hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="9aeb1-115">Gli autori consentono la limitazione e il controllo di accesso con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="9aeb1-116">Ogni client di hub eventi viene assegnato un token univoco, che viene caricato toohello client.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="9aeb1-117">Hello token vengono prodotti in modo che ognuno concede l'accesso tooa univoco server di pubblicazione diverso.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="9aeb1-118">Un client che dispone di un token può inviare solo tooone server di pubblicazione, ma nessun altro server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="9aeb1-119">Se più client Condivisione hello stesso token, quindi ognuno di essi condivide un server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="9aeb1-120">Sebbene non sia consigliabile, è possibile tooequip dispositivi con i token che concedono l'hub di eventi di accesso diretto tooan.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="9aeb1-121">Qualsiasi dispositivo che contiene un token di questo tipo può inviare messaggi direttamente a tale hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="9aeb1-122">Il dispositivo non sarà soggetto toothrottling.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="9aeb1-123">Inoltre, il dispositivo di hello non è possibile impedire l'invio di hub di eventi toothat.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="9aeb1-124">Tutti i token sono firmati con una chiave SAS.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="9aeb1-125">In genere, tutti i token sono firmati con hello stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="9aeb1-126">I client non sono a conoscenza della chiave di hello; Ciò impedisce ad altri client di produrre token.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="9aeb1-127">Creare la chiave di firma di accesso condiviso hello</span><span class="sxs-lookup"><span data-stu-id="9aeb1-127">Create hello SAS key</span></span>

<span data-ttu-id="9aeb1-128">Quando si crea uno spazio dei nomi dell'hub eventi, il servizio di hello genera una chiave di firma di accesso condiviso a 256 bit denominata **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="9aeb1-129">Questa chiave concede inviano, ascolto e gestire lo spazio dei nomi toohello di diritti.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="9aeb1-130">È anche possibile creare chiavi aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-130">You can also create additional keys.</span></span> <span data-ttu-id="9aeb1-131">È consigliabile creare una chiave che concede l'hub di eventi specifici toohello di autorizzazioni di invio.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="9aeb1-132">In seguito hello in questo argomento, si presuppone che questa chiave è denominato **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="9aeb1-133">Hello di esempio seguente crea una chiave di solo invio durante la creazione di hub eventi hello:</span><span class="sxs-lookup"><span data-stu-id="9aeb1-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="9aeb1-134">Generare token</span><span class="sxs-lookup"><span data-stu-id="9aeb1-134">Generate tokens</span></span>

<span data-ttu-id="9aeb1-135">È possibile generare token usando una chiave SAS hello.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="9aeb1-136">È necessario ottenere solo un token per client.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-136">You must produce only one token per client.</span></span> <span data-ttu-id="9aeb1-137">I token possono essere creati utilizzando hello al metodo.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="9aeb1-138">Tutti i token vengono generati utilizzando hello **EventHubSendKey** chiave.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="9aeb1-139">A ogni token viene assegnato un URI univoco.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="9aeb1-140">Quando si chiama questo metodo, hello URI deve essere specificato come `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="9aeb1-141">Per tutti i token, è identico, con l'eccezione hello di hello URI `PUBLISHER_NAME`, che deve essere diverso per ogni token.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="9aeb1-142">Idealmente, `PUBLISHER_NAME` rappresenta hello ID del client hello che riceve il token.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="9aeb1-143">Questo metodo genera un token con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="9aeb1-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="9aeb1-144">ora di scadenza del token Hello è espresso in secondi dal 1 ° gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="9aeb1-145">Hello Ecco un esempio di un token:</span><span class="sxs-lookup"><span data-stu-id="9aeb1-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="9aeb1-146">In genere, i token hello hanno una durata uguale o maggiore durata hello del client hello.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="9aeb1-147">Se client hello dispone di un nuovo token hello funzionalità tooobtain, è possono utilizzare i token con una durata più breve.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="9aeb1-148">Invio di dati</span><span class="sxs-lookup"><span data-stu-id="9aeb1-148">Sending data</span></span>
<span data-ttu-id="9aeb1-149">Dopo avere creato il token hello, viene eseguito il provisioning di ogni client con il proprio token univoco.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="9aeb1-150">Quando il client di hello invia dati a un hub eventi, è la richiesta di trasmissione con token hello di tag.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="9aeb1-151">un attacco intercetti e rubi il token di hello, la comunicazione tra client hello e hub eventi hello hello tooprevent devono essere eseguite tramite un canale crittografato.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="9aeb1-152">Disattivazione dei client</span><span class="sxs-lookup"><span data-stu-id="9aeb1-152">Blacklisting clients</span></span>
<span data-ttu-id="9aeb1-153">Se il furto di un token da un utente malintenzionato, hello può rappresentare client hello è stato rubato il token.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="9aeb1-154">La disattivazione di un client rende il rendering di tale client inutilizzabile fino a che non riceve un nuovo token che usa un autore diverso.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="9aeb1-155">Autenticazione delle applicazioni back-end</span><span class="sxs-lookup"><span data-stu-id="9aeb1-155">Authentication of back-end applications</span></span>

<span data-ttu-id="9aeb1-156">applicazioni back-end tooauthenticate che utilizzano i dati di hello generati dai client di hub eventi, gli hub eventi Usa un modello di sicurezza che è simile modello toohello utilizzato per gli argomenti del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="9aeb1-157">Un gruppo di consumer dell'hub eventi è l'argomento del Bus di servizio tooa sottoscrizione tooa equivalente.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="9aeb1-158">Un client può creare un gruppo di consumer se il gruppo di consumer hello toocreate hello richiesta è accompagnato da un token che concede privilegi per l'hub di eventi hello di gestione o per hello dello spazio dei nomi toowhich hub eventi hello appartiene.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="9aeb1-159">Un client è consentito tooconsume dati da un gruppo di consumer se hello ricevere la richiesta sono accompagnati da un token che concede diritti per questo gruppo di consumer di ricezione, hello hub eventi o hub eventi di hello dello spazio dei nomi toowhich hello appartiene.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="9aeb1-160">versione corrente di Hello del Bus di servizio non supporta le regole di firma di accesso condiviso per singole sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="9aeb1-161">Hello che stesso vale per i gruppi di consumer di hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="9aeb1-162">Verrà aggiunto il supporto di firma di accesso condiviso per entrambe le funzionalità in hello future.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="9aeb1-163">In assenza di hello di autenticazione SAS per gruppi di consumer singoli, è possibile utilizzare toosecure chiavi SAS tutti i gruppi di consumer con una chiave comune.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="9aeb1-164">Questo approccio consente un tooconsume dati dell'applicazione da uno qualsiasi dei gruppi di consumer hello di un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="9aeb1-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aeb1-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9aeb1-165">Next steps</span></span>
<span data-ttu-id="9aeb1-166">toolearn più sugli hub di eventi, visitare hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="9aeb1-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="9aeb1-167">[Panoramica di Hub eventi]</span><span class="sxs-lookup"><span data-stu-id="9aeb1-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="9aeb1-168">[Panoramica delle firme di accesso condiviso]</span><span class="sxs-lookup"><span data-stu-id="9aeb1-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="9aeb1-169">[Applicazioni di esempio che usano Hub eventi]</span><span class="sxs-lookup"><span data-stu-id="9aeb1-169">[Sample applications that use Event Hubs]</span></span>

[Panoramica di Hub eventi]: event-hubs-what-is-event-hubs.md
[Applicazioni di esempio che usano Hub eventi]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Panoramica delle firme di accesso condiviso]: ../service-bus-messaging/service-bus-sas.md

