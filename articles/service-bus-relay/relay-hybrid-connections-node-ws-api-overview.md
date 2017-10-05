---
title: Panoramica delle API Node di inoltro di Azure | Microsoft Docs
description: Panoramica dell'API Node di inoltro
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="6afd7-103">Panoramica dell'API del pacchetto Node per Connessioni ibride di inoltro</span><span class="sxs-lookup"><span data-stu-id="6afd7-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="6afd7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6afd7-104">Overview</span></span>

<span data-ttu-id="6afd7-105">Il pacchetto Node [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) per le connessioni ibride di inoltro di Azure si basa sul pacchetto NPM ['ws'](https://www.npmjs.com/package/ws) e lo estende.</span><span class="sxs-lookup"><span data-stu-id="6afd7-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="6afd7-106">Questo pacchetto permette di esportare nuovamente tutte le esportazioni del pacchetto di base e aggiunge nuove esportazioni che consentono l'integrazione con la funzionalità connessioni ibride del servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="6afd7-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="6afd7-107">Le applicazioni esistenti che usano `require('ws')` possono usare questo pacchetto con `require('hyco-ws')`, che consente scenari ibridi in cui un'applicazione può contemporaneamente restare in attesa di connessioni WebSocket in locale dall'interno del firewall e tramite connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="6afd7-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="6afd7-108">Documentazione</span><span class="sxs-lookup"><span data-stu-id="6afd7-108">Documentation</span></span>

<span data-ttu-id="6afd7-109">La documentazione delle API si trova [nel pacchetto 'ws' principale](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="6afd7-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="6afd7-110">Questo articolo descrive le differenze tra questo pacchetto e il pacchetto di base.</span><span class="sxs-lookup"><span data-stu-id="6afd7-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="6afd7-111">La differenza principale tra il pacchetto di base e questo pacchetto 'hyco-ws' sta nell'aggiunta di una nuova classe server, esportata tramite `require('hyco-ws').RelayedServer`, e alcuni metodi helper.</span><span class="sxs-lookup"><span data-stu-id="6afd7-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="6afd7-112">Metodi helper del pacchetto</span><span class="sxs-lookup"><span data-stu-id="6afd7-112">Package helper methods</span></span>

<span data-ttu-id="6afd7-113">Nell'esportazione del pacchetto sono disponibili diversi metodi di utilità a cui è possibile fare riferimento come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6afd7-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="6afd7-114">I metodi helper sono progettati per questo pacchetto, ma possono essere usati anche da un server Node per abilitare client di dispositivo o Web per la creazione di listener o mittenti.</span><span class="sxs-lookup"><span data-stu-id="6afd7-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="6afd7-115">Il server ne fa uso passando a questi metodi URI che incorporano token di breve durata.</span><span class="sxs-lookup"><span data-stu-id="6afd7-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="6afd7-116">È possibile usare questi URI anche con stack WebSocket comuni che non supportano l'impostazione di intestazioni HTTP per l'handshake WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6afd7-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="6afd7-117">L'incorporamento di token di autorizzazione nell'URI è supportato principalmente per scenari di utilizzo esterni alla libreria.</span><span class="sxs-lookup"><span data-stu-id="6afd7-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="6afd7-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="6afd7-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6afd7-119">Crea un URI del listener della connessione ibrida di inoltro di Azure valido per il percorso e lo spazio dei nomi specificati.</span><span class="sxs-lookup"><span data-stu-id="6afd7-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="6afd7-120">L'URI può quindi essere usato con la versione di inoltro della classe WebSocketServer.</span><span class="sxs-lookup"><span data-stu-id="6afd7-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="6afd7-121">`namespaceName` (obbligatorio): nome di dominio completo dello spazio dei nomi di inoltro di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="6afd7-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="6afd7-122">`path` (obbligatorio): nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6afd7-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6afd7-123">`token` (facoltativo): token di accesso di inoltro rilasciato in precedenza incorporato nell'URI del listener. Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="6afd7-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="6afd7-124">`id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.</span><span class="sxs-lookup"><span data-stu-id="6afd7-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6afd7-125">Il valore `token` è facoltativo e deve essere usato solo quando non è possibile inviare intestazioni HTTP con l'handshake WebSocket, come nel caso dello stack WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="6afd7-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="6afd7-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="6afd7-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6afd7-127">Crea un URI di invio della connessione ibrida di inoltro di Azure valido per il percorso e lo spazio dei nomi specificati.</span><span class="sxs-lookup"><span data-stu-id="6afd7-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="6afd7-128">L'URI può essere usato con qualsiasi client WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6afd7-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="6afd7-129">`namespaceName` (obbligatorio): nome di dominio completo dello spazio dei nomi di inoltro di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="6afd7-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="6afd7-130">`path` (obbligatorio): nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6afd7-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6afd7-131">`token` (facoltativo): token di accesso di inoltro rilasciato in precedenza incorporato nell'URI di invio. Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="6afd7-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="6afd7-132">`id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.</span><span class="sxs-lookup"><span data-stu-id="6afd7-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6afd7-133">Il valore `token` è facoltativo e deve essere usato solo quando non è possibile inviare intestazioni HTTP con l'handshake WebSocket, come nel caso dello stack WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="6afd7-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="6afd7-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="6afd7-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6afd7-135">Crea un token di firma di accesso condiviso di inoltro di Azure per l'URI di destinazione specificato, una regola di firma di accesso condiviso e la relativa chiave. Quest'ultima è valida per il numero di secondi specificato o per un'ora dall'istante corrente, se viene omesso l'argomento della scadenza.</span><span class="sxs-lookup"><span data-stu-id="6afd7-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="6afd7-136">`uri` (obbligatorio): URI per il quale viene rilasciato il token.</span><span class="sxs-lookup"><span data-stu-id="6afd7-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="6afd7-137">L'URI viene normalizzato affinché usi lo schema HTTP e le informazioni sulla stringa di query vengono rimosse.</span><span class="sxs-lookup"><span data-stu-id="6afd7-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="6afd7-138">`ruleName` (obbligatorio): nome della regola di firma di accesso condiviso per l'entità rappresentata dall'URI specificato o per lo spazio dei nomi rappresentato dalla parte dell'URI relativa all'host.</span><span class="sxs-lookup"><span data-stu-id="6afd7-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="6afd7-139">`key` (obbligatorio): chiave valida della regola di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="6afd7-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="6afd7-140">`expirationSeconds` (facoltativo): numero di secondi fino alla scadenza del token generato.</span><span class="sxs-lookup"><span data-stu-id="6afd7-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="6afd7-141">Se non viene specificato, il valore predefinito è 1 ora (3600).</span><span class="sxs-lookup"><span data-stu-id="6afd7-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="6afd7-142">Il token rilasciato conferisce i diritti associati alla regola di firma di accesso condiviso specificata per la durata specificata.</span><span class="sxs-lookup"><span data-stu-id="6afd7-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="6afd7-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="6afd7-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6afd7-144">A livello funzionale, questo metodo equivale al metodo `createRelayToken` documentato in precedenza, ma restituisce il token aggiunto in modo corretto all'URI di input.</span><span class="sxs-lookup"><span data-stu-id="6afd7-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="6afd7-145">Class ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="6afd7-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="6afd7-146">La classe `hycows.RelayedServer` rappresenta un'alternativa alla classe `ws.Server`, che non rimane in ascolto sulla rete locale ma delega l'ascolto al servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="6afd7-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="6afd7-147">Le due classi sono per lo più compatibili a livello di contratto. Ciò significa che un'applicazione esistente che usa la classe `ws.Server` può essere modificata facilmente per l'uso della versione inoltrata.</span><span class="sxs-lookup"><span data-stu-id="6afd7-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="6afd7-148">Le differenze principali sono rappresentate dal costruttore e dalle opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="6afd7-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="6afd7-149">Costruttore</span><span class="sxs-lookup"><span data-stu-id="6afd7-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="6afd7-150">Il costruttore `RelayedServer` supporta un set di argomenti diverso rispetto a `Server`, perché non è un listener autonomo né può essere incorporato in un framework di listener HTTP esistente.</span><span class="sxs-lookup"><span data-stu-id="6afd7-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="6afd7-151">Anche il numero di opzioni disponibili è ridotto, perché la gestione del WebSocket viene delegata in gran parte al servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="6afd7-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="6afd7-152">Argomenti del costruttore:</span><span class="sxs-lookup"><span data-stu-id="6afd7-152">Constructor arguments:</span></span>

- <span data-ttu-id="6afd7-153">`server` (obbligatorio): URI completo del nome di una connessione ibrida su cui rimanere in ascolto, costruito in genere con il metodo helper WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="6afd7-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="6afd7-154">`token` (obbligatorio): questo argomento contiene una stringa di token rilasciata in precedenza o una funzione di callback che è possibile chiamare per ottenere la stringa di token.</span><span class="sxs-lookup"><span data-stu-id="6afd7-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="6afd7-155">È preferibile usare l'opzione di callback, perché consente il rinnovo del token.</span><span class="sxs-lookup"><span data-stu-id="6afd7-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="6afd7-156">Eventi</span><span class="sxs-lookup"><span data-stu-id="6afd7-156">Events</span></span>

<span data-ttu-id="6afd7-157">Le istanze di `RelayedServer` generano tre eventi che consentono di gestire le richieste in ingresso, stabilire le connessioni e rilevare le condizioni di errore.</span><span class="sxs-lookup"><span data-stu-id="6afd7-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="6afd7-158">Per gestire i messaggi è necessario sottoscrivere l'evento `connect`.</span><span class="sxs-lookup"><span data-stu-id="6afd7-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="6afd7-159">headers</span><span class="sxs-lookup"><span data-stu-id="6afd7-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="6afd7-160">L'evento `headers` viene generato immediatamente prima che venga accettata una connessione in ingresso, consentendo la modifica delle intestazioni da inviare al client.</span><span class="sxs-lookup"><span data-stu-id="6afd7-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="6afd7-161">connessione</span><span class="sxs-lookup"><span data-stu-id="6afd7-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="6afd7-162">Viene generato quando viene accettata una nuova connessione WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6afd7-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="6afd7-163">L'oggetto è di tipo `ws.WebSocket`, come nel pacchetto di base.</span><span class="sxs-lookup"><span data-stu-id="6afd7-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="6afd7-164">error</span><span class="sxs-lookup"><span data-stu-id="6afd7-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="6afd7-165">Se il server sottostante genera un errore, viene inoltrato qui.</span><span class="sxs-lookup"><span data-stu-id="6afd7-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="6afd7-166">Helper</span><span class="sxs-lookup"><span data-stu-id="6afd7-166">Helpers</span></span>

<span data-ttu-id="6afd7-167">Per semplificare l'avvio di un server inoltrato e sottoscrivere immediatamente le connessioni in ingresso, il pacchetto espone una semplice funzione helper che viene usata anche negli esempi, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6afd7-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="6afd7-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="6afd7-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="6afd7-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="6afd7-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="6afd7-170">Questo metodo chiama il costruttore per creare una nuova istanza di RelayedServer e quindi sottoscrive il callback specificato nell'evento 'connection'.</span><span class="sxs-lookup"><span data-stu-id="6afd7-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="6afd7-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="6afd7-171">relayedConnect</span></span>

<span data-ttu-id="6afd7-172">Con il semplice mirroring dell'helper `createRelayedServer` nella funzione, `relayedConnect` crea una connessione client e sottoscrive l'evento 'open' nel socket risultante.</span><span class="sxs-lookup"><span data-stu-id="6afd7-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="6afd7-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6afd7-173">Next steps</span></span>
<span data-ttu-id="6afd7-174">Per altre informazioni sul servizio di inoltro di Azure, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6afd7-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="6afd7-175">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="6afd7-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6afd7-176">API di inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="6afd7-176">Available Relay APIs</span></span>](relay-api-overview.md)
