---
title: aaaOverview di hello Azure inoltro nodo API | Documenti Microsoft
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
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="a7585-103">Panoramica dell'API del pacchetto Node per Connessioni ibride di inoltro</span><span class="sxs-lookup"><span data-stu-id="a7585-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="a7585-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a7585-104">Overview</span></span>

<span data-ttu-id="a7585-105">Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacchetto nodo per le connessioni ibride di inoltro di Azure si basa su ed estende hello ['ws'](https://www.npmjs.com/package/ws) pacchetto NPM.</span><span class="sxs-lookup"><span data-stu-id="a7585-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="a7585-106">Questo pacchetto consente di esportare nuovamente tutte le esportazioni di tale pacchetto di base e aggiunge nuove esportazioni che consentono l'integrazione con funzionalità connessioni ibride del servizio di inoltro Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="a7585-107">Le applicazioni esistenti che `require('ws')` possibile utilizzare questo pacchetto con `require('hyco-ws')` , invece, consentendo anche scenari ibridi in cui un'applicazione può restare in ascolto per le connessioni di WebSocket localmente da "all'interno di firewall hello" e tramite le connessioni ibride, tutto Hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="a7585-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="a7585-108">Documentazione</span><span class="sxs-lookup"><span data-stu-id="a7585-108">Documentation</span></span>

<span data-ttu-id="a7585-109">Hello API sono [documentati nel pacchetto principale 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="a7585-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="a7585-110">Questo articolo descrive le differenze tra questo pacchetto e il pacchetto di base.</span><span class="sxs-lookup"><span data-stu-id="a7585-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="a7585-111">Hello principali differenze tra il pacchetto base hello e questa 'hyco-ws' è quello di aggiungere una nuova classe server, esportata tramite `require('hyco-ws').RelayedServer`e alcuni metodi di supporto.</span><span class="sxs-lookup"><span data-stu-id="a7585-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="a7585-112">Metodi helper del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a7585-112">Package helper methods</span></span>

<span data-ttu-id="a7585-113">Durante l'esportazione di pacchetti hello che è possibile fare riferimento come indicato di seguito sono disponibili diversi metodi di utilità:</span><span class="sxs-lookup"><span data-stu-id="a7585-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="a7585-114">metodi helper Hello sono da utilizzare con questo pacchetto, ma sono inoltre utilizzabile da un nodo server per l'abilitazione di listener di toocreate client web o un dispositivo o i mittenti.</span><span class="sxs-lookup"><span data-stu-id="a7585-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="a7585-115">server Hello utilizza questi metodi passando l'URI che incorporano i token di breve durati.</span><span class="sxs-lookup"><span data-stu-id="a7585-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="a7585-116">Gli URI possono essere usati anche con gli stack di WebSocket comuni che non supportano le intestazioni HTTP di impostazione per l'handshake WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="a7585-117">Incorporamento di token di autorizzazione in hello che URI è supportato principalmente per gli scenari di utilizzo della libreria esterna.</span><span class="sxs-lookup"><span data-stu-id="a7585-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="a7585-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="a7585-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="a7585-119">Crea un listener di connessione ibrida di Azure inoltro URI valido per lo spazio dei nomi e percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="a7585-120">Questo URI è quindi utilizzabile con la versione di hello inoltro di hello WebSocketServer classe.</span><span class="sxs-lookup"><span data-stu-id="a7585-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="a7585-121">`namespaceName`(obbligatorio) - hello Nome dominio completo di hello Azure inoltro dello spazio dei nomi toouse.</span><span class="sxs-lookup"><span data-stu-id="a7585-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="a7585-122">`path`(obbligatorio) - hello nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="a7585-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="a7585-123">`token`(facoltativo): un accesso emesso in precedenza di inoltro del token che è incorporato nel listener hello URI (vedere il seguente esempio hello).</span><span class="sxs-lookup"><span data-stu-id="a7585-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="a7585-124">`id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.</span><span class="sxs-lookup"><span data-stu-id="a7585-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="a7585-125">Hello `token` valore è facoltativo e deve essere utilizzato solo quando non è possibile toosend HTTP intestazioni insieme handshake WebSocket hello, come accade hello con lo stack di hello WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="a7585-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="a7585-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="a7585-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="a7585-127">Crea una trasmissione connessione ibrida di Azure inoltro URI valida per hello specificato dello spazio dei nomi e il percorso.</span><span class="sxs-lookup"><span data-stu-id="a7585-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="a7585-128">L'URI può essere usato con qualsiasi client WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a7585-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="a7585-129">`namespaceName`(obbligatorio) - hello Nome dominio completo di hello Azure inoltro dello spazio dei nomi toouse.</span><span class="sxs-lookup"><span data-stu-id="a7585-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="a7585-130">`path`(obbligatorio) - hello nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="a7585-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="a7585-131">`token`inviare un token di accesso emesso in precedenza di inoltro incorporato in hello (facoltativo) - URI (vedere il seguente esempio hello).</span><span class="sxs-lookup"><span data-stu-id="a7585-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="a7585-132">`id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.</span><span class="sxs-lookup"><span data-stu-id="a7585-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="a7585-133">Hello `token` valore è facoltativo e deve essere utilizzato solo quando non è possibile toosend HTTP intestazioni insieme handshake WebSocket hello, come accade hello con lo stack di hello WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="a7585-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="a7585-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="a7585-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="a7585-135">Crea un token di Azure inoltro condiviso (firma di accesso) per l'URI di destinazione specificato hello, regola SAS e chiave di firma di accesso condiviso regola valida per hello dato numero di secondi o per un'ora da hello corrente immediata se hello scadenza viene omesso.</span><span class="sxs-lookup"><span data-stu-id="a7585-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="a7585-136">`uri`(obbligatorio) - hello URI per il quale hello token è toobe rilasciato.</span><span class="sxs-lookup"><span data-stu-id="a7585-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="a7585-137">Hello URI è lo schema HTTP di hello toouse normalizzato e informazioni sulla stringa di query viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="a7585-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="a7585-138">`ruleName`(obbligatorio) - nome per l'entità hello rappresentata da hello URI di base di regola SAS o hello dello spazio dei nomi rappresentato da hello parte host URI.</span><span class="sxs-lookup"><span data-stu-id="a7585-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="a7585-139">`key`(obbligatorio) - chiave valido per la regola di firma di accesso condiviso di hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="a7585-140">`expirationSeconds`(facoltativo): numero di hello di secondi prima hello generato token avranno una scadenza.</span><span class="sxs-lookup"><span data-stu-id="a7585-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="a7585-141">Se non specificato, il valore predefinito di hello è 1 ora (3600).</span><span class="sxs-lookup"><span data-stu-id="a7585-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="a7585-142">il token emesso Hello conferisce diritti hello associati hello specificato regola SAS per hello ha durata.</span><span class="sxs-lookup"><span data-stu-id="a7585-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="a7585-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="a7585-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="a7585-144">Questo metodo è funzionalmente equivalente toohello `createRelayToken` metodo documentato in precedenza, ma restituisce hello token URI di input toohello accodato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a7585-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="a7585-145">Class ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="a7585-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="a7585-146">Hello `hycows.RelayedServer` classe è un'alternativa toohello `ws.Server` classe che non è in ascolto sulla rete locale hello ma delega toohello in ascolto il servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7585-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="a7585-147">le classi di Hello due sono principalmente contratto compatibile, il che significa che un'applicazione esistente usando hello `ws.Server` classe può essere facilmente modificati toouse versione di hello inoltrata.</span><span class="sxs-lookup"><span data-stu-id="a7585-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="a7585-148">Hello principali differenze riguardano nel costruttore hello in opzioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="a7585-149">Costruttore</span><span class="sxs-lookup"><span data-stu-id="a7585-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="a7585-150">Hello `RelayedServer` costruttore supporta un set diverso di argomenti di hello `Server`, perché non è un listener autonomo o in grado di toobe incorporato in un framework di listener HTTP esistente.</span><span class="sxs-lookup"><span data-stu-id="a7585-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="a7585-151">Sono disponibili anche meno opzioni poiché hello gestione WebSocket è in gran parte delegata toohello servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="a7585-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="a7585-152">Argomenti del costruttore:</span><span class="sxs-lookup"><span data-stu-id="a7585-152">Constructor arguments:</span></span>

- <span data-ttu-id="a7585-153">`server`(obbligatorio) - hello completo URI per un nome della connessione ibrida in cui toolisten, in genere costruiti con il metodo di supporto WebSocket.createRelayListenUri() hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="a7585-154">`token`(obbligatorio) - questo argomento contiene una stringa di token emessa in precedenza o una funzione di callback che può essere chiamata tooobtain questo tipo è una stringa di token.</span><span class="sxs-lookup"><span data-stu-id="a7585-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="a7585-155">opzione di callback Hello è consigliabile, poiché consente di rinnovo del token.</span><span class="sxs-lookup"><span data-stu-id="a7585-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="a7585-156">Events</span><span class="sxs-lookup"><span data-stu-id="a7585-156">Events</span></span>

<span data-ttu-id="a7585-157">`RelayedServer`istanze generano tre eventi che consentono di toohandle le richieste in ingresso, stabiliscono le connessioni e rilevare le condizioni di errore.</span><span class="sxs-lookup"><span data-stu-id="a7585-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="a7585-158">È necessario sottoscrivere toohello `connect` toohandle i messaggi di evento.</span><span class="sxs-lookup"><span data-stu-id="a7585-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="a7585-159">headers</span><span class="sxs-lookup"><span data-stu-id="a7585-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="a7585-160">Hello `headers` evento viene generato immediatamente prima una connessione in ingresso viene accettata, abilitare la modifica del client di hello intestazioni toosend toohello.</span><span class="sxs-lookup"><span data-stu-id="a7585-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="a7585-161">connessione</span><span class="sxs-lookup"><span data-stu-id="a7585-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="a7585-162">Viene generato quando viene accettata una nuova connessione WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a7585-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="a7585-163">oggetto Hello è di tipo `ws.WebSocket`, uguale a quello con il pacchetto base hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="a7585-164">error</span><span class="sxs-lookup"><span data-stu-id="a7585-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="a7585-165">Se server sottostante hello genera un errore, viene inoltrato qui.</span><span class="sxs-lookup"><span data-stu-id="a7585-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="a7585-166">Helper</span><span class="sxs-lookup"><span data-stu-id="a7585-166">Helpers</span></span>

<span data-ttu-id="a7585-167">toosimplify avviare immediatamente la sottoscrizione tooincoming connessioni, hello e un server inoltrato al pacchetto espone una funzione helper semplice, che viene inoltre utilizzata negli esempi di hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a7585-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="a7585-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="a7585-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="a7585-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="a7585-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="a7585-170">Questo metodo chiama hello costruttore toocreate una nuova istanza di hello RelayedServer e quindi sottoscritta hello fornito callback toohello 'connessione' evento.</span><span class="sxs-lookup"><span data-stu-id="a7585-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="a7585-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="a7585-171">relayedConnect</span></span>

<span data-ttu-id="a7585-172">Mirroring semplicemente hello `createRelayedServer` helper in funzione, `relayedConnect` crea una connessione di client e sottoscrive l'evento 'open' toohello socket risultante hello.</span><span class="sxs-lookup"><span data-stu-id="a7585-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7585-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7585-173">Next steps</span></span>
<span data-ttu-id="a7585-174">toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a7585-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="a7585-175">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="a7585-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a7585-176">API di inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="a7585-176">Available Relay APIs</span></span>](relay-api-overview.md)
