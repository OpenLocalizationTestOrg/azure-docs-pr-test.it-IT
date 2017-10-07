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
# <a name="relay-hybrid-connections-node-api-overview"></a>Panoramica dell'API del pacchetto Node per Connessioni ibride di inoltro

## <a name="overview"></a>Panoramica

Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacchetto nodo per le connessioni ibride di inoltro di Azure si basa su ed estende hello ['ws'](https://www.npmjs.com/package/ws) pacchetto NPM. Questo pacchetto consente di esportare nuovamente tutte le esportazioni di tale pacchetto di base e aggiunge nuove esportazioni che consentono l'integrazione con funzionalità connessioni ibride del servizio di inoltro Azure hello. 

Le applicazioni esistenti che `require('ws')` possibile utilizzare questo pacchetto con `require('hyco-ws')` , invece, consentendo anche scenari ibridi in cui un'applicazione può restare in ascolto per le connessioni di WebSocket localmente da "all'interno di firewall hello" e tramite le connessioni ibride, tutto Hello stesso tempo.
  
## <a name="documentation"></a>Documentazione

Hello API sono [documentati nel pacchetto principale 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md). Questo articolo descrive le differenze tra questo pacchetto e il pacchetto di base. 

Hello principali differenze tra il pacchetto base hello e questa 'hyco-ws' è quello di aggiungere una nuova classe server, esportata tramite `require('hyco-ws').RelayedServer`e alcuni metodi di supporto.

### <a name="package-helper-methods"></a>Metodi helper del pacchetto

Durante l'esportazione di pacchetti hello che è possibile fare riferimento come indicato di seguito sono disponibili diversi metodi di utilità:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

metodi helper Hello sono da utilizzare con questo pacchetto, ma sono inoltre utilizzabile da un nodo server per l'abilitazione di listener di toocreate client web o un dispositivo o i mittenti. server Hello utilizza questi metodi passando l'URI che incorporano i token di breve durati. Gli URI possono essere usati anche con gli stack di WebSocket comuni che non supportano le intestazioni HTTP di impostazione per l'handshake WebSocket hello. Incorporamento di token di autorizzazione in hello che URI è supportato principalmente per gli scenari di utilizzo della libreria esterna. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Crea un listener di connessione ibrida di Azure inoltro URI valido per lo spazio dei nomi e percorso di hello. Questo URI è quindi utilizzabile con la versione di hello inoltro di hello WebSocketServer classe.

- `namespaceName`(obbligatorio) - hello Nome dominio completo di hello Azure inoltro dello spazio dei nomi toouse.
- `path`(obbligatorio) - hello nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.
- `token`(facoltativo): un accesso emesso in precedenza di inoltro del token che è incorporato nel listener hello URI (vedere il seguente esempio hello).
- `id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.

Hello `token` valore è facoltativo e deve essere utilizzato solo quando non è possibile toosend HTTP intestazioni insieme handshake WebSocket hello, come accade hello con lo stack di hello WebSocket W3C.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Crea una trasmissione connessione ibrida di Azure inoltro URI valida per hello specificato dello spazio dei nomi e il percorso. L'URI può essere usato con qualsiasi client WebSocket.

- `namespaceName`(obbligatorio) - hello Nome dominio completo di hello Azure inoltro dello spazio dei nomi toouse.
- `path`(obbligatorio) - hello nome di una connessione ibrida di inoltro di Azure esistente nello spazio dei nomi.
- `token`inviare un token di accesso emesso in precedenza di inoltro incorporato in hello (facoltativo) - URI (vedere il seguente esempio hello).
- `id` (facoltativo): identificatore di rilevamento che consente di tenere traccia della diagnostica end-to-end delle richieste.

Hello `token` valore è facoltativo e deve essere utilizzato solo quando non è possibile toosend HTTP intestazioni insieme handshake WebSocket hello, come accade hello con lo stack di hello WebSocket W3C.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Crea un token di Azure inoltro condiviso (firma di accesso) per l'URI di destinazione specificato hello, regola SAS e chiave di firma di accesso condiviso regola valida per hello dato numero di secondi o per un'ora da hello corrente immediata se hello scadenza viene omesso.

- `uri`(obbligatorio) - hello URI per il quale hello token è toobe rilasciato. Hello URI è lo schema HTTP di hello toouse normalizzato e informazioni sulla stringa di query viene rimossa.
- `ruleName`(obbligatorio) - nome per l'entità hello rappresentata da hello URI di base di regola SAS o hello dello spazio dei nomi rappresentato da hello parte host URI.
- `key`(obbligatorio) - chiave valido per la regola di firma di accesso condiviso di hello. 
- `expirationSeconds`(facoltativo): numero di hello di secondi prima hello generato token avranno una scadenza. Se non specificato, il valore predefinito di hello è 1 ora (3600).

il token emesso Hello conferisce diritti hello associati hello specificato regola SAS per hello ha durata.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Questo metodo è funzionalmente equivalente toohello `createRelayToken` metodo documentato in precedenza, ma restituisce hello token URI di input toohello accodato correttamente.

### <a name="class-wsrelayedserver"></a>Class ws.RelayedServer

Hello `hycows.RelayedServer` classe è un'alternativa toohello `ws.Server` classe che non è in ascolto sulla rete locale hello ma delega toohello in ascolto il servizio di inoltro di Azure.

le classi di Hello due sono principalmente contratto compatibile, il che significa che un'applicazione esistente usando hello `ws.Server` classe può essere facilmente modificati toouse versione di hello inoltrata. Hello principali differenze riguardano nel costruttore hello in opzioni disponibili hello.

#### <a name="constructor"></a>Costruttore  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Hello `RelayedServer` costruttore supporta un set diverso di argomenti di hello `Server`, perché non è un listener autonomo o in grado di toobe incorporato in un framework di listener HTTP esistente. Sono disponibili anche meno opzioni poiché hello gestione WebSocket è in gran parte delegata toohello servizio di inoltro.

Argomenti del costruttore:

- `server`(obbligatorio) - hello completo URI per un nome della connessione ibrida in cui toolisten, in genere costruiti con il metodo di supporto WebSocket.createRelayListenUri() hello.
- `token`(obbligatorio) - questo argomento contiene una stringa di token emessa in precedenza o una funzione di callback che può essere chiamata tooobtain questo tipo è una stringa di token. opzione di callback Hello è consigliabile, poiché consente di rinnovo del token.

#### <a name="events"></a>Events

`RelayedServer`istanze generano tre eventi che consentono di toohandle le richieste in ingresso, stabiliscono le connessioni e rilevare le condizioni di errore. È necessario sottoscrivere toohello `connect` toohandle i messaggi di evento. 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

Hello `headers` evento viene generato immediatamente prima una connessione in ingresso viene accettata, abilitare la modifica del client di hello intestazioni toosend toohello. 

##### <a name="connection"></a>connessione

```JavaScript
function(socket)
```

Viene generato quando viene accettata una nuova connessione WebSocket. oggetto Hello è di tipo `ws.WebSocket`, uguale a quello con il pacchetto base hello.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Se server sottostante hello genera un errore, viene inoltrato qui.  

#### <a name="helpers"></a>Helper

toosimplify avviare immediatamente la sottoscrizione tooincoming connessioni, hello e un server inoltrato al pacchetto espone una funzione helper semplice, che viene inoltre utilizzata negli esempi di hello, come indicato di seguito:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Questo metodo chiama hello costruttore toocreate una nuova istanza di hello RelayedServer e quindi sottoscritta hello fornito callback toohello 'connessione' evento.
 
##### <a name="relayedconnect"></a>relayedConnect

Mirroring semplicemente hello `createRelayedServer` helper in funzione, `relayedConnect` crea una connessione di client e sottoscrive l'evento 'open' toohello socket risultante hello.

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

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:
* [Che cos'è il servizio di inoltro di Azure?](relay-what-is-it.md)
* [API di inoltro disponibili](relay-api-overview.md)
